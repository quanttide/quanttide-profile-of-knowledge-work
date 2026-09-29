# 阿里云 OSS 静态站点部署问题记录

2026-09-26 为 qtgame-tycoon 部署站点（`tycoon.game.quanttide.com`）时踩到的问题与解法。模式以 quanttide-platform 的 `static-site`、`cdn-auth` 模块为准，本文记录该模式之外的坑，供后续建站直接复用。

## 问题与解决

### 公共读设置被账号级防护拦截

现象：新建桶设公共读时 ACL 与 Bucket Policy 均返回 403，分别为 `Put public bucket acl is not allowed` 与 `Put public bucket policy is not allowed`。用户属 `admin` 组（AdministratorAccess）且 developers 组有 `AliyunOSSFullAccess`，因此不是 RAM 权限问题，而是账号级防护，CLI 无法关闭。

解决：放弃公共读，走 quanttide-platform 的既定模式——桶保持私有，CDN 开 `l2_oss_key` 私有回源（`private_oss_auth=on`）。账号级角色 `AliyunCDNAccessingPrivateOSSRole` 已由 `modules/cdn-auth` 创建过一次，全账号站点共享，直接复用即可。CI 上传用 AccessKey 不受影响，公网访问全部经 CDN 鉴权回源。

### 根路径回源 403

现象：`/index.html` 等对象路径回源正常（响应头 `x-oss-cdn-auth: success`），但根路径 `/` 返回 403，错误为 `You are forbidden to list buckets`——CDN 把 `/` 当作 OSS 列举请求回源，回源鉴权不覆盖该请求。

解决：配置 `back_to_origin_url_rewrite`，把 `/` 及未知路径改写为 `/index.html`（`flag: break`，`source_url` 用负向断言正则排除真实产物）。配置后根路径与深链均返回 200。排查方法是找一个同模式的线上域名（如 `strategy.quanttide.com`）做配置 diff，差异即答案。

### 二级域名证书不覆盖

现象：`*.quanttide.com` 泛证书只覆盖一层子域，不覆盖 `tycoon.game.quanttide.com`；quanttide-platform 的 `ssl-cert.yml` SAN 清单也不含 `*.game.quanttide.com`，直接复用会导致 HTTPS 无法建立。

解决：本机 acme.sh 以 DNS-01 签发 `*.game.quanttide.com`（Let's Encrypt 拒绝通配符与显式同名域名同时下单，只保留通配符即可），用 `aliyun cdn SetCdnDomainSSLCertificate` 绑定，并新增 `~/.acme.sh/deploy-cdn-cert-tycoon.sh` 作为 `--reloadcmd`，续期成功后自动重新绑定。该脚本与既有的 `deploy-cdn-cert-health.sh`、`deploy-cdn-cert-data-studio.sh` 同款。

### aliyun CLI 使用细节

- `DescribeCdnDomainConfigs` 的 `--FunctionNames` 是逗号分隔的字符串，传 JSON 数组会报误导性的 `InvalidFunctionName.ValueNotSupported`，功能名本身是有效的；
- 单域名功能配置没有 Set API，用 `BatchSetCdnDomainConfig`（`--DomainNames` 加 `--Functions`，函数 JSON 内含 `functionName` 与 `functionArgs`）；
- `aliyun oss set-acl` 设桶级 ACL 需要 `-b` 选项，否则按对象路径解析报错；
- `acme.sh` 的子命令写作 `--issue`，写成 `issue` 会被错误解析成密钥名；
- CDN 域名的备案号 Description 字段无 CLI 参数可设，只能在控制台填写。

## 最终配置清单

1. 创建私有桶并开静态网站托管（默认首页 `index.html`，错误页按站点需要设定）；
2. CDN 接入域名，源站指向 `<bucket>.oss-cn-hangzhou.aliyuncs.com`（类型 oss，端口 80）；
3. 依次配置三个功能：`l2_oss_key` 私有回源、`https_force` 强制跳转、`back_to_origin_url_rewrite` 根路径改写；
4. 在 `quanttide.com` 解析下添加 `CNAME` 记录指向域名的 `*.w.kunlunaq.com`；
5. 签发并绑定覆盖域名的证书，配置 reloadcmd 保证续期自动重绑；
6. 用 `curl` 验证四条：DNS 解析、HTTP 301、HTTPS 200、根路径返回站点首页。

## 相关参考

- quanttide-platform：`manifests/terraform/modules/static-site`、`manifests/terraform/modules/cdn-auth`、`docs/dev-guide/iac/websites.md`
- 本机证书链：`~/.acme.sh/deploy-cdn-cert-tycoon.sh`
- 站点 CI：qtgame-tycoon 仓库 `.github/workflows/deploy-site.yml`（头注释含前置条件清单）

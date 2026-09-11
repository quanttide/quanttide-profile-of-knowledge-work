# DevOps 发布

给 QtCloud Work CLI 走一次预发布——定预发布版本号、收 CHANGELOG、跑四道门禁、发布预检、`--dry-run` 预演、人点头、真发、核 tag 已推。工作区根是领域仓，判据里的路径从仓根算。

产物是本任务的报告，缺省落草稿区；要进正式仓就在任务文件的 `products.report` 里写 `data/report/iGuo/<名字>.md`。

## 步骤与验收

### version 定版本

输入 `apps/qtcloud-work/src/cli/Cargo.toml` 里的现有版本与 `CHANGELOG.md` 的 `[Unreleased]`；定预发布版本号（`X.Y.Z-pre.N`，正式发布前的每一次都用它递增），把 Unreleased 收成 `## [X.Y.Z-pre.N]` 一节并写进这次变更，Cargo.toml 的 `version` 跟着改。

验收：程序查 `CHANGELOG.md`、`Cargo.toml` 都在，变更记录里有 Cargo.toml 里那个版本的条目，且 tag 前缀与版本对得上；智能体审版本号、CHANGELOG 条目、Cargo.toml 三处一致，条目里写清了这次变更、不是空条目。

### gate 质量门禁

逐道跑四道门禁，红了就修到绿，修完从文档改起（要改行为先改文档与测试）。结果写进报告的「门禁」一节。

验收：程序逐道跑 `cargo fmt --check`、`cargo clippy --all-targets -- -D warnings`、`cargo test --quiet`、`sh scripts/validate-usecases.sh`，四道全绿，且报告里有「## 门禁」一节。

### audit 发布预检

跑 `qtcloud-devops release audit`（版本号格式、配置文件一致性、CHANGELOG、工作区是否干净、标签冲突、远程可达、已有 Release），逐项清到全过，条款输出抄进报告的「预检」一节。

验收：程序跑 `qtcloud-devops release audit` 全过，且报告里有「## 预检」一节。

### rehearse 预演

跑 `qtcloud-devops release publish --dry-run`，看清它会建哪个 tag、推去哪、发到哪个仓；把预演输出抄进报告的「预演」一节。产出任何东西都算失败——预演不建 tag、不推、不发 Release。

验收：程序跑预演跑得通、期间没有多出 tag，且报告里有「## 预演」一节；智能体审预演输出说清了会建哪个 tag、发去哪、发布范围是哪几个提交。

### confirm 人点头

创始人看一遍版本号、变更范围、将建的 tag，确认无误后在报告的「结论」一节写明「可以发布」与版本号。

验收：程序查报告「## 结论」里有版本与放行；人拍创始人确认版本号与变更范围，放行这次预发布。

### publish 真发

跑 `qtcloud-devops release publish -y`（校验 CHANGELOG → 建 tag → 推远端 → 建 GitHub Release），把结果抄进报告的「发布」一节。

验收：程序跑发布跑完、tag 已在远端，且报告里有「## 发布」一节；智能体审报告里写清了这次发布的 tag、Release 地址与它对应哪些变更。

## 产物

本任务的报告，含门禁、预检、预演、结论、发布各一节；远端是新建的 tag 与 Release。

## 怎么跑

```bash
qtcloud-work task --new devops-release --workflow devops-release
```

再 `qtcloud-work task devops-release --next`，一条一条走。

# DevOps 发布

给 QtCloud Work CLI 走一次预发布——定预发布版本号、收 CHANGELOG、跑四道门禁、发布预检、`--dry-run` 预演、人点头、真发、核 tag 已推。工作区根是领域仓，判据里的路径从仓根算。

产物是本任务的报告，缺省落草稿区；要进正式仓就在任务文件的 `products.report` 里写 `data/report/iGuo/<名字>.md`。

## 六步

1. version——定版本：把 `apps/qtcloud-work/src/cli/Cargo.toml` 的版本与 `CHANGELOG.md` 的 `[Unreleased]` 收成 `## [X.Y.Z-pre.N]` 一节，三处一致。
2. gate——质量门禁：`cargo fmt --check`、`cargo clippy --all-targets -- -D warnings`、`cargo test`、`validate-usecases.sh` 逐道跑绿，红了从文档改起。
3. audit——发布预检：`qtcloud-devops release audit` 逐项清到全过，条款输出抄进报告「预检」一节。
4. rehearse——预演：`qtcloud-devops release publish --dry-run`，看清会建哪个 tag、推去哪、发到哪个仓；预演不建 tag、不推、不发 Release。
5. confirm（人）——人点头：创始人看一遍版本号、变更范围、将建的 tag，确认后在报告「结论」一节写明「可以发布」与版本号。
6. publish——真发：`qtcloud-devops release publish -y`，走校验 CHANGELOG、建 tag、推远端、建 GitHub Release；tag 已在远端才算过。

## 产物

本任务的报告，含门禁、预检、预演、结论、发布各一节；远端是新建的 tag 与 Release。

## 怎么跑

```bash
qtcloud-work task --new devops-release --workflow devops-release
```

再 `qtcloud-work task devops-release --next`，一条一条走。

# Rust 测试命名惯例

**文件与目标**：`tests/` 下每个文件是一个独立的测试目标，文件名以**被测对象**命名，全小写下划线，不带 `scenario_`、`usecase_`、`test_` 这类前缀——`task_start.rs`、`run_context.rs`，不是 `scenario_start_task.rs`。测私有实现的小测试留在源码里，用 `#[cfg(test)] mod tests`，不占 `tests/`。

**共用夹具**：放 `tests/common/mod.rs`。`tests/` 顶层的每个 `.rs` 都会被当成一个测试目标编译，夹具只有放进子目录才不会被单独编译；各文件用 `mod common;` 引入。

**测试函数名**：小写下划线，描述「做什么、预期什么」，读起来是一句话；`#[test]` 已经说明它是测试，名字里不再写 `test_`，也不写场景编号。条件写进名字里：`start_task_lays_down_files_and_context`、`one_step_with_three_kinds_of_criteria`、`take_one_agent_step_through_pi`。

**一个场景一个文件，同类合并**：一个场景一个文件；同一场景的正例与它的反例放在**同一个**测试函数里。反例单独成测，在实现还没写时会先变绿，就成了空壳。

**出处注释**：文件头用 `//!` 写这个文件测哪一条用例（场景一句话），紧贴 `#[test]` 上方一行写 `// 用例：一`。对账脚本按这个格式抓（`scripts/validate-usecases.sh`：文档里的用例号与测试里的出处号必须相等）。

**断言与失败信息**：`assert!(cond, "…{}", run.crop())`——失败时把退出码与两路输出一并打出来，别只报「不相等」。

**不碰真东西**：跑编出来的二进制，用临时目录当工作区与数据仓；外部命令用桩脚本顶替（如 `pi` 桩），测试不依赖真模型、真服务、真仓库。

**门禁**：`cargo test` 全绿；`cargo fmt --check` 与 `cargo clippy -- -D warnings` 两绿——本地从严，与 CI 一致。

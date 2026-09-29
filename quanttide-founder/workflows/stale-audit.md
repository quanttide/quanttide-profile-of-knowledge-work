# 资源落后检测

不定期找出落后于实现的资源——规格、案例、手册、user-guide 等。这些资源是 AI 写程序时会读的，一旦落后，旧信息就喂给了 AI，而你往往当场注意不到。所以能机器查的尽量机器查，查不了的再由智能体对着真值逐条核。

触发看水位不看日历——实现侧改了（改 API / 改命令名 / 发版）、资源侧改了术语、AI 要开工读某几篇前、距上次体检一个周期，任一出现就跑一次。

## scan 打样

列出 AI 写程序时会读的资源：规格在 `docs/specification`、案例在 `docs/gallery`、手册在 `docs/handbook`、user-guide 在 `packages/quanttide-work-toolkit/docs/user-guide`。挑出本次要核的入口几篇，写进报告「抽查清单」一节，并点明每篇的真值源。

验收：报告里有「抽查清单」一节（程序，`{{report}}` 含 `## 抽查清单`）；每篇都点明真值源——源码 / 契约向量 / 命令 `--help` / 规范（智能体）。

## run-checks 跑检查

跑得动的都实跑：工具箱的文档示例与契约向量、画廊各工作流 yaml 的校验、全仓相对链接可达性。命令与结论写进报告同一节。

验收：文档示例与测试对得上（程序，`sh packages/quanttide-work-toolkit/scripts/doc-tests.sh`）；两侧契约向量都过（程序，`sh packages/quanttide-work-toolkit/scripts/contract.sh`）；跑不了的检查说明原因，不留空过（智能体）。

## diff-truth 对真值

逐条核命名、字段、取值（以源码与契约向量为准）、命令与示例（以实跑为准）、版本号与清单（以 `Cargo.toml` / `pubspec.yaml` / `package.json` 为准），把「资源 → 落后点 → 真值 → 怎么改」写进报告「落后清单」一节。

验收：报告里有「落后清单」一节（程序，`{{report}}` 含 `## 落后清单`）；每条落后项都给出真值与改法（智能体）。

## fix 修

把资源改到与真值一致：改规格、改案例、改手册、改 user-guide，改版本号与旧名（如 `kg` / `find` 一类已弃用称法）。需拍板的单列出来。

验收：资源仓有改动（程序，`git status --porcelain -- docs packages` 非空）；清单里每条落后项都有处置——改了，或列在待拍板（智能体）；需拍板的落后项由创始人定（人）。

## commit 落账提交

各资源仓分别提交推送（工具箱、规范、画廊、手册等），再逐层更新父仓指针；结果抄进 `data/report`。

验收：相关指针都已记录，子模块内容脏不算，看指针（程序，`git status --porcelain --ignore-submodules=dirty -- docs packages` 为空）；创始人点头——落后项都处置了（人）。

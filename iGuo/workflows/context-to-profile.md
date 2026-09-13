# 语境到档案

把新到的语境条目粗加工成个人档案的材料——拉语境、逐条认归属、写进材料库、把已迁出的从语境删掉、分层提交。产物是本任务的报告：`data/context/qtcloud-work/artifacts/report/context-to-profile.md`。

## pull 拉语境

把语境拉到最新（`git -C data/context pull --ff-only`），把新到的日期文件逐条读一遍，清单写进报告的「条目清单」一节。

验收：语境能拉到最新（程序，`git -C data/context pull --ff-only` 成功）；条目清单写进报告（程序，`{{report}}` 含 `## 条目清单`）。

## classify 认归属

逐条认归属：每条归到材料库的哪个分类——agent 智能体、connect 沟通、infra 基础设施、work 知识工作、org 组织管理、write 写作、meta 元工程、course 课程。把「条目 → 分类」写进报告的同一节，拿不准的单列出来。

验收：每条都有着落——进了某个分类，或列在「拿不准」里（智能体）；拿不准的分类由创始人裁决（人）。

## coarsen 粗加工

粗加工进材料：每条口语流水收成「标签：内容」的一节，写进 `data/profile/iGuo/materials/<分类>/index.md`；分类目录不在就新建，里面放 `index.md`。一条一意、平实陈述。

验收：材料库有改动（程序，`git -C data/profile status --porcelain -- iGuo/materials` 非空）；每条都进了对应分类，写法平实，没有「不是…而是…」式表达（智能体）。

## move-out 迁出语境

迁出语境：已进材料的条目从语境日期文件里删掉，日期文件留空、目录保留；没处理的条目留着。

验收：语境仓有改动，迁出落到文件上（程序，`git -C data/context status --porcelain` 非空）。

## commit 分层提交

分层提交推送：材料在档案仓提交推送，迁出在语境仓提交推送，再回工作区更新 `data/profile` 与 `data/context` 两个指针。

验收：两个指针都已记录，子模块内容脏不算，看指针（程序，`git status --porcelain --ignore-submodules=dirty` 对 `data/profile`、`data/context` 为空）；创始人点头——分类与迁出都对（人）。

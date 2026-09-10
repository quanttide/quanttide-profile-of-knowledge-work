# 报告：compare-course-profile

## 定位

两边档案都找齐了，各自坐标与内容如下。

### 个人课程草稿：`iGuo/materials/course/`

共 3 个 Markdown，是个人随笔式草稿：

- [`index.md`](../../materials/course/index.md)：**量潮课堂**目录，挂两门课
- [`knowledge-work.md`](../../materials/course/knowledge-work.md)：**知识工作**——方法论课（自举/打通/验证三层）
- [`production-internship.md`](../../materials/course/production-internship.md)：**生产实习**——实战课（指导边界、壳作 baseline）

形态：单文件口语化叙述，无课时编号、无 JSON、无验收标准。

### 课程研发档案：`../../../quanttide-course/data/profile/`

即 `/home/iguo/repos/quanttide/domains/quanttide-course/data/profile/`，自述为课程内容的「唯一创作源头」。

- `README.md`：量潮课程研发档案
- `AGENTS.md` / `CONTRIBUTING.md`：约定「单源双格式」（MD 给人、JSON 给机器）、课时目录 `lessonN-<slug>`
- `data-engineering/index.md`：数据工程课程需求（理论 24 学时、实验 8 学时、实践待安排）
- `production-internship/`：`README.md` 占位 + `lesson1-second-brain/`（`index.md` + `index.json`，3 个场景）
- `vibe-coding/`：`lesson1-zed/`（index + 3 个场景的 md/json，含 mp4 与 html DAG 视图）、`lesson2-feishu/`、`lesson3-github/`

形态：每课时一目录，`index.md` + `index.json` 成对，场景文件 `0X-<scene>.*`。

### 判据核对

- 个人课程草稿在：`iGuo/materials/course/index.md` ✓
- 课程研发档案在：`../../../quanttide-course/data/profile/README.md` ✓

## 比对

口径、重叠、缺口、格式，四面照。

### 口径

- **个人课程草稿**：以「量潮课堂」为验证组织的产品构思——用体系教体系，课程是验证「知识工作产出质量是否可见提升」的手段。
- **课程研发档案**：以生产实习为中心的课程内容源头——产出可直接上架的课时（Markdown 给人、JSON 给机器），口径是教学交付。

### 重叠

| 课 | 个人草稿 | 课程研发档案 |
|----|---------|-------------|
| **生产实习**（production-internship） | 制度与验证思路：指导边界（群体/个体、免费/付费）、壳即 baseline、观察不纠正 | 有课程目录但 README 是占位；仅 `lesson1-second-brain` 一课时，讲用量潮第二大脑完成开工作区与逐级提交 |
| **知识工作**（knowledge-work） | 方法论课：自举/打通/验证三层，作业即 PR | 无同名课程；档案里最近的是生产实习课时1（第二大脑实操），未承载「方法论课」定位 |
| **氛围编程**（vibe-coding） | 未提及 | `lesson1-zed`（环境）、`lesson2-feishu`（协作）、`lesson3-github`（开源），三课时齐全 |
| **数据工程**（data-engineering） | 未提及 | 只有需求（理论 24 学时、实验 8 学时、实践待安排），无课时 |

重叠只在「生产实习」这条课程名上，内容层几乎不交叠：草稿给的是制度与验证口径，档案给的是可执行课时。

### 缺口

**个人课程草稿的缺口**：

- 无课时/场景结构、无编号；无验收标准，全是散文式理念。
- 无机器可读格式（JSON），不能直接上架。
- 覆盖不全：`量潮课堂` 目录只挂知识工作、生产实习两门，缺 vibe-coding、data-engineering。
- 知识工作没有对应落地形态；生产实习只有制度/验证思路，无可跟做的步骤。

**课程研发档案的缺口**：

- data-engineering 只有需求与学时，零课时、零场景。
- production-internship 只有 lesson1，README 仍是占位；草稿里的「指导边界制度」「壳 baseline」没有变成课时或验收标准。
- 缺「量潮课堂」这一层：验证目标、风险、回报机制在档案里没有对应设计。
- vibe-coding README 只有标题，课程说明缺失。
- AGENTS.md 索引里的 `index.md`（研发策略）在本仓库实际不存在，链接悬空。

### 格式差

| 面 | 个人草稿 | 课程研发档案 |
|----|---------|-------------|
| 组织 | 扁平单文件（3 篇 MD） | 每课程一目录，每课时 `lessonN-<slug>/` |
| 命名 | 中文文件名 | 目录英文小写连字符 |
| 载体 | 只有 Markdown | `index.md` + `index.json` 成对，场景另有 md/json（vibe-coding 还带 mp4 与 html DAG 视图） |
| 结构 | 无表格、无图、无字段 | 场景表 + mermaid DAG + `acceptance{criteria, method, on_fail}` |

附注：档案自身的 `CONTRIBUTING.md` 仍写旧结构（`lesson1.json` + `lesson1/index.md` + `sense1.md`），与实际目录（`lessonN-<slug>/` + `index.json` + `0X-<scene>.*`）不一致，是一处待还的格式债。

## 结论

**总原则**：课程研发档案（`quanttide-course/data/profile`）是课程内容的唯一创作源头；个人草稿是概念与制度层，不整篇搬过去，只把能课程化的部分回流。个人档案保留构思与验证设计的原貌。

### 回流：草稿 → 课程研发档案

| 草稿里的东西 | 回流到 | 形式 |
|----|----|----|
| 「知识工作」方法论课（自举/打通/验证三层、作业即 PR） | 档案里新开一门 `knowledge-work/`，或并入生产实习作为方法论总纲 | 先写课程 README + 一课时 `lesson1-*` 的 `index.md`/`index.json`，别只留理念 |
| 生产实习的「壳 baseline」观察法 | `production-internship/` 的验收标准设计 | 写进课时 `index.md` 的 acceptance：验收通不过先修标准，不纠正学生 |
| 指导边界（群体免费/个体付费、反馈发生在提交时点） | `production-internship/README.md` 的课程边界口径 | 三两句话，不做成独立制度文档 |

### 不并：留在个人档案

「量潮课堂」验证组织本身——验证目标（产出质量是否可见提升）、风险（日志流于形式）、回报机制——属验证组织/主体层的设计，不是课程内容，不并入档案。

### 不动：档案里的存量

- `vibe-coding/` 三课时：草稿无对应，保持原样。
- `data-engineering/index.md` 需求：保持原样，等课时填充。
- `production-internship/lesson1-second-brain`：保持原样，回流内容新增课时而非改写它。

### 顺手要还的格式债（与回流分开）

- `CONTRIBUTING.md` 旧结构（`lesson1.json` + `sense1.md`）与实际 `lessonN-<slug>/` 不一致。
- `AGENTS.md` 里的 `index.md`（研发策略）链接悬空，实际文件不存在。

### 请创始人拍板

1. 「知识工作」是**新开一门课**，还是并入生产实习作为方法论总纲？
2. 指导边界制度只作为课程边界口径回流，还是根本不属于课程、另立主体层文档？
3. 「量潮课堂」验证设计留在个人档案，还是另开一份产品/验证文档单独承载？

## 执行记录

- ✓ 2026-09-10 22:31　开工　对比个人课程草稿与课程研发档案
- ✓ 2026-09-10 22:32　locate　两边档案找齐：个人草稿 iGuo/materials/course/（3 篇 MD）；课程研发档案 ../../../quanttide-course/data/profile/（3 门课，MD+JSON）；两条判据命中
- ✓ 2026-09-10 22:32　locate　AI 执行：locate 一步完成：两边档案都找齐并写进报告——个人课程草稿在 `iGuo/materials/course/`（index、knowledge-work、
- ✓ 2026-09-10 22:32　compare　AI 执行：compare 一步完成：在报告 `iGuo/artifacts/report/compare-course-profile.md` 新增「## 比对」一节，按
- ✓ 2026-09-10 22:33　conclude　AI 执行：一句话：我把差异处置结论写进了报告「结论」一节，等创始人就回流与并法点头。

## 比对」一节，按

## 闸门项

- ⧗ 创始人点头（回流与并法怎么定）（留给人 / 待判）

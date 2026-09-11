# 课程档案比对

个人档案里的课程草稿是内部版本，量潮课程研发档案是正式版本。这条工作流把两边摆到一起，看口径、重叠、各自的缺口与格式差，然后定下差异怎么处置。

## 三步

1. locate——把两边档案找齐。个人草稿在 `iGuo/materials/course/`，正式档案在 `../../../quanttide-course/data/profile/`。判据是两边各有目录文件在，程序自己检查。
2. compare——逐项对照，结果写进报告 `iGuo/artifacts/report/compare-course-profile.md` 的「比对」一节。判据是报告里点到两边的课，并且给出了两侧缺口。
3. conclude——写下差异怎么处置：谁回流给谁、哪些并、哪些不动；写进同一份报告的「结论」一节，再请创始人拍板。判据一条是程序检查 `## 结论` 在不在，一条是留给人的闸门项。

三步都由智能体执行。判据里有两条留给人：创始人点头。

## 产物

报告在 `iGuo/artifacts/report/compare-course-profile.md`，其中「执行记录」「闸门项」两节由程序维护，其余各节归人与智能体。日志在 `iGuo/artifacts/journal/compare-course-profile.md`，记这次工作的来龙去脉。

## 怎么跑

```bash
kg --root <本档案> --data <本档案>/iGuo task compare-course-profile --next
```

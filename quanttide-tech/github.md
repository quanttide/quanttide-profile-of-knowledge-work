# quanttide-tech 的 GitHub 结构

quanttide-tech 主体在 GitHub 组织 `quanttide-tech` 下分公开、私有两仓：公开仓收主体公开档案，私有仓是工作台，用子模块把各业务线的私有数据挂在一起。本文记录私有仓的子模块结构。

## 两仓

- `quanttide-tech/quanttide-tech`——公开仓，主体公开档案
- `quanttide-tech/quanttide-tech-private`——私有仓，工作台；本文记录对象

## 子模块

| 路径 | 仓库 | 分支 | 指针 |
|:-----|:-----|:-----|:-----|
| `assets/public` | `quanttide-tech/quanttide-tech` | main | eb1ee31 |
| `data/qtadmin-private` | `quanttide-tech/qtadmin-private` | （未指定） | 7c4a3b0 |
| `data/qtalliance-private` | `quanttide-tech/qtalliance-private` | main | 376a757 |
| `data/qtclass-private` | `quanttide-tech/qtclass-private` | main | 231f4e5 |
| `data/qtcloud-private` | `quanttide-tech/qtcloud-private` | main | c7ab6f8 |
| `data/qtconsult-private` | `quanttide-tech/qtconsult-private` | main | eb28e88 |
| `data/qtcrowd-private` | `quanttide-tech/qtcrowd-private` | main | fff59fd |
| `data/qtdata-private` | `quanttide-tech/qtdata-private` | main | f9d5ad3 |
| `data/qtrecurit-private` | `quanttide-tech/qtrecurit-private` | main | ba38abf |

## 说明

- `assets/public` 挂的是公开仓本身：私有仓通过这一挂载同时持有公开资产，与「私有转公开」路线（`quanttide-tech/default/roadmap/private-to-public.md`）对应。
- `data/qt*-private` 每条业务线一个私有仓，命名 `qt{业务线}-private`；`qtadmin-private` 未在 `.gitmodules` 指定分支，随父仓指针走。
- 私有仓 README 的「子项目入口」仍写 `apps/qt*-private`，实际挂载在 `data/qt*-private`，以 `.gitmodules` 为准；`apps/` 已空。

## 快照

- 记录时间：2026-10-23
- 父仓：`quanttide-tech-private` @ 5a2738e（main）

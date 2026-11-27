# 第 0 周：准备（11/26 ～ 11/29）

**目标**：板子到货前把软件侧全部就绪，到货当天就能烧写验证。
**验收**：VM 能编译；SDK 源码 `repo` 检出完成；**出厂镜像点亮板子**（串口有 log、屏有画面）。
**投入**：本周只有 4 天且板子 11/29 才到，按 8–10h 算。

## 任务清单

### 环境（板子到货前必须完成）

- [ ] 装 VMware + Ubuntu **20.04 desktop**（用 A 盘自带 ISO，不下载）
- [ ] VM 规格：系统盘 60G + 数据盘 150G、内存主机一半、vCPU 4–6、**网络桥接**、关 3D 加速、开时间同步
- [ ] `apt update` 若报 404 / `Release file expired` → 改旧归档源（记录进 [docs/environment.md](../docs/environment.md)）
- [ ] 装依赖（命令见计划第 0 周）+ `repo` 工具
- [ ] `sudo systemctl set-default multi-user.target`（默认不进桌面）
- [ ] 打快照 `snap0-clean`
- [ ] 解压 SDK → **`./repo.sh` 检出源码**（解压 ≠ 检出）
- [ ] 打快照 `snap1-src`
- [ ] Windows 侧：RKDevTool、CH343SER 驱动、MobaXterm、VS Code + Remote-SSH

### TF 卡

- [ ] 备份卡里原有的 Pi OS 数据（刷写会**清空整张卡**）
- [ ] 用 SDDiskTool / Rufus / Etcher 刷 `rk3506b_update_sd.img`（A 盘 `09、系统镜像`）
- [ ] 记下：卡容量、烧写工具、耗时 → 填 [docs/bringup.md](../docs/bringup.md) 烧写记录表

### 板子到货后（11/29 周日）

- [ ] 开箱检查：板子、屏、配件、丝印版本
- [ ] 上电 + 串口连上（115200），看到启动 log
- [ ] 网口、USB、屏逐一确认
- [ ] 填 [hardware/board.md](../hardware/board.md) 的清单与接口记录

## 每日记录

<!-- 每天收工前加一节，三行即可：卡在哪 / 怎么解决 / 明天第一步 -->

### 11/27（周五）· 待填 h

- 卡在：
- 解决：
- 明天第一步：

## 本周产出

| 类型 | 内容 | 位置 |
| --- | --- | --- |
| 环境 | VM 规格与依赖 | [docs/environment.md](../docs/environment.md) |
| 代码 | — | — |
| 截图 / log | 首个串口启动 log | [docs/bringup.md](../docs/bringup.md) |

## 复盘（周日）

| 项 | 计划 | 实际 |
| --- | --- | --- |
| 投入小时 | 8–10 | |
| 快照数 | 2 | |
| 板子是否点亮 | 是 | |

- 掉队原因：
- 下周调整：

## 面试问答（本周能讲清的 3 个问题）

1. 为什么要用 Ubuntu 20.04 而不是最新的？你的环境里哪些东西和 SDK 版本绑定？
2. `repo` 检出和 `tar` 解压在版本管理上有什么区别？
3. 为什么编译放 VM、烧写放 Windows？（USB 透传 / 救砖可靠性）

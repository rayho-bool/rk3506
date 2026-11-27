# RK3506 嵌入式 Linux 学习仓

在正点原子 ATK-DLRK3506B 上，从「跟课跑例程」走到「独立交付一个可演示项目」的八周记录。
学习计划见 [RK3506-八周学习计划.md](RK3506-八周学习计划.md)。

**目标**：八周后能回答两个问题——「给你一块空板子，从零到能演示要几天？」「dts 里这个外设的四条链路分别从原理图哪来？」

---

## 进度

| 周 | 日期 | 主题 | 状态 | 记录 |
| --- | --- | --- | --- | --- |
| 0 | 11/26–11/29 | 环境 / 源码 / 出厂镜像 | 🟡 进行中 | [weeks/week0.md](weeks/week0.md) |
| 1 | 11/30–12/06 | 编译与烧写 | ⬜ | [weeks/week1.md](weeks/week1.md) |
| 2 | 12/07–12/13 | 交叉编译与应用开发 | ⬜ | [weeks/week2.md](weeks/week2.md) |
| 3 | 12/14–12/20 | Linux 系统编程 | ⬜ | [weeks/week3.md](weeks/week3.md) |
| 4 | 12/21–12/27 | 硬件接口（GPIO / I2C / CAN） | ⬜ | [weeks/week4.md](weeks/week4.md) |
| 5 | 12/28–01/03 | 字符设备驱动 + 选题冻结 | ⬜ | [weeks/week5.md](weeks/week5.md) |
| 6 | 01/04–01/10 | 异构 AMP（弹性） | ⬜ | [weeks/week6.md](weeks/week6.md) |
| 7 | 01/11–01/17 | 项目实现（LVGL 1.5 天） | ⬜ | [weeks/week7.md](weeks/week7.md) |
| 8 | 01/18–01/24 | 收尾 | ⬜ | [weeks/week8.md](weeks/week8.md) |

状态：⬜ 未开始 ／ 🟡 进行中 ／ ✅ 完成 ／ ⏭ 跳过

## 硬件

| 项 | 型号 | 状态 |
| --- | --- | --- |
| 开发板 | 正点原子 ATK-DLRK3506B | 已发货，预计 **11/29（周日）** 到 |
| 屏幕 | ATK-MD0550M 5.5" MIPI 720×1280 | 已购 |
| 存储 | TF 卡（原刷 Pi OS，需重刷 SD 镜像） | 1 张，建议再买一张 32G 备用 |

详见 [hardware/board.md](hardware/board.md)。

## 环境

VMware + Ubuntu 20.04 desktop（默认不进图形界面），桥接网络，原生编译；烧写和串口在 Windows 侧。
详见 [docs/environment.md](docs/environment.md)。

## 目录

```
├── RK3506-八周学习计划.md   # 计划 v2
├── README.md                # 本文件：进度 / 工作流 / 复现步骤
├── docs/
│   ├── environment.md       # VM 规格、依赖、快照、常用命令
│   ├── bringup.md           # 启动链、烧写记录、救砖
│   ├── architecture.md      # 项目架构（第 5 周冻结）
│   └── resources.md         # 资料索引
├── hardware/
│   └── board.md             # 硬件清单、接口使用、引脚分配
├── weeks/
│   └── week0.md … week8.md  # 每周任务 + 每日记录 + 复盘 + 面试问答
├── src/                     # 自己写的代码
└── 0/                       # 厂商资料（不进 git，见 .gitignore）
```

---

## 怎么用这个仓库

### 每天收工前（10 分钟）

1. 打开本周的 `weeks/weekN.md`，在「每日记录」下加一节：

   ```markdown
   ### 11/30（周日）· 3h

   - 卡在：`build.sh lunch` 之后全量编译在 u-boot 阶段报 `openssl/ssl.h not found`
   - 解决：`apt install libssl-dev` 后重编，通过
   - 明天第一步：烧写出厂镜像确认串口
   ```

   **三行就够，不要写成日记。** 重点是把「卡住的原文报错」抄下来——第 8 周写 README 和第 2 周你自己回头查，靠的都是这句。

2. 有代码就提交：

   ```bash
   git add -A
   git commit -m "w1: 全量编译通过，产物在 build/output"
   ```

### 每周日（20 分钟）

1. 勾完本周任务清单，填「本周产出」和「复盘（计划 vs 实际小时）」
2. 更新 [README.md](README.md) 进度表的状态列
3. 打标记并备份：

   ```bash
   git tag w1-done
   git push --tags
   ```

4. 遇到值得记住的部署/环境变更，同步到 `docs/environment.md` 或 `docs/bringup.md`

### 什么时候写 docs 下的文件

| 文件 | 什么时候动 |
| --- | --- |
| `docs/environment.md` | 环境有任何变化（改 apt 源、装新工具、打快照） |
| `docs/bringup.md` | 每次烧写前后；救砖成功后必须写 |
| `docs/architecture.md` | 第 5 周必须填完；之后只允许小改 |
| `docs/resources.md` | 发现新资料时追加 |
| `hardware/board.md` | 用到一个新接口/新引脚就加一行 |

### 什么进仓库、什么不进

| 进 | 不进 |
| --- | --- |
| 自己写的 C / Python / shell 代码 | 厂商资料 `0/`（已 ignore，几个 G） |
| 笔记、架构图、引脚表（文本/mermaid） | 编译产物 `build/`、`output/`、`*.img`、`*.bin`、`*.ko` |
| 关键串口 log 的**摘录**（十几行） | 完整 log 文件（几百 MB，用 `*.log` 已 ignore） |
| 波形截图、界面截图（PNG，单张 < 1MB） | 录屏视频（放外部链接，例如 B 站） |

> 判断标准：**换一台电脑 clone 下来，能否在新机器上复现我的工作？** 能就进，不能就想想是不是该写成文字。

### 提交信息约定

```
w<周次>: <做了什么>          # w1: 全量编译通过
fix: <修了什么>              # fix: 内核模块 insmod 报版本不符
docs: <改了哪份文档>          # docs: 补启动链图
env: <环境变更>              # env: apt 源改 old-releases
```

一个人开发不用开分支，直接 `main`；用 `git tag` 标记里程碑即可。

### 备份（重要）

VM 会坏、硬盘会坏。本仓库已绑 **三个远端**：

| 名字 | 位置 | 用途 |
| --- | --- | --- |
| `origin` | <https://gitee.com/rayho_bool/rk3506.git> | 主，日常 push；本地 `master` 跟踪它 |
| `github` | <https://github.com/rayho-bool/rk3506.git> | 平台备份（**必须保持私有**） |
| `backup` | `D:\rk3506-backup.git`（本机裸仓库） | 离线备份，不依赖网络 |

每周日推一次：

```powershell
git push origin master --tags
git push github master --tags
git push backup master --tags
```

三条规则：

1. **别对两个远端都 `push --force`。** force 只影响你指定的那一个，但两边历史一旦分叉，补救很麻烦
2. **分叉了先看再动**：`git fetch --all` → `git log --graph --all`，确认哪边是你想要的
3. **填 IP / 密码之前，确认 `github` 那个仓是私有的。** 公开仓里的敏感信息删不干净（会被爬、被 fork）

---

## 复现步骤

> 第 8 周填。目标：别人拿到这个仓库，照着这一段能从零跑到演示。

1. 装 VMware + Ubuntu 20.04 desktop，配置见 [docs/environment.md](docs/environment.md)
2. 装依赖（命令见 [RK3506-八周学习计划.md](RK3506-八周学习计划.md) 第 0 周）
3. 取 SDK，`./repo.sh` 检出，`./build.sh lunch` 选 `<填编号>`，`./build.sh`
4. 烧写 `<填介质与工具>`，串口 115200
5. 编译 `src/<项目目录>`，部署到板子
6. 运行与验证：`<填命令与预期输出>`

# 第 5 周：字符设备驱动 + 选题冻结（12/28 ～ 01/03）

**目标**：写出一个能加载、能控制硬件的字符设备驱动；**同时把项目选题与架构冻结**。
**验收**：LED 驱动可通过 `write` 控制亮灭，dts 里 GPIO 配好；`docs/architecture.md` 填完并打 tag `arch-frozen`。
**投入**：16h（元旦周，强度略降，但选题不能拖）

> 为什么这周就冻结选题：第 7 周只有 5 天，边设计边实现会两样都做不好。

## 任务清单

### 驱动

- [ ] 字符设备框架：`file_operations`、`register_chrdev`、`cdev`
- [ ] 实现 `open/read/write/ioctl/release`
- [ ] 理解 `copy_to_user` / `copy_from_user`，为什么不能直接解引用用户指针
- [ ] `platform_driver` + 设备树匹配（`compatible` 字符串对不上会静默不 probe，学会看 `/sys/bus/platform`）
- [ ] 用 `gpiod_get` / `gpio_request` 在驱动里点灯
- [ ] `printk` 日志级别 + `dmesg -w` 实时看
- [ ] ⭐ 用 `miscdevice` 简化写法
- [ ] ⭐ dynamic debug：不改代码打开某个 `pr_debug`

### 项目

- [ ] 从三个题目里选一个（理由写进 architecture.md，**只选已跑通模块的组合**）
- [ ] 画架构图 + 数据流表
- [ ] 定义「内核 ↔ 应用」接口与「应用 ↔ 上位机」协议
- [ ] 写清超时 / 重连 / 校验三项取值与理由
- [ ] `git tag arch-frozen` 并 push

## 每日记录

<!-- 每天收工前加一节，三行即可：卡在哪 / 怎么解决 / 明天第一步 -->

### 待填 · 待填 h

- 卡在：
- 解决：
- 明天第一步：

## 本周产出

| 类型 | 内容 | 位置 |
| --- | --- | --- |
| 代码 | LED 字符设备驱动 + dts 片段 | `src/led-driver/` |
| 文档 | 项目架构（冻结） | [docs/architecture.md](../docs/architecture.md) |

## 复盘（周日）

| 项 | 计划 | 实际 |
| --- | --- | --- |
| 投入小时 | 16 | |
| 驱动加载成功 | 是 | |
| 选题是否冻结 | 是 | |

- 掉队原因：
- 下周调整：

## 面试问答（本周能讲清的 3 个问题）

1. 一个字符设备从 `insmod` 到用户态能 `open` 到它，中间发生了什么？
2. `copy_to_user` 为什么不能用 `memcpy` 代替？
3. `platform_driver` 和 `platform_device`（或 dts 节点）怎么匹配上的？不匹配怎么排查？

# 第 4 周：硬件接口（12/21 ～ 12/27）

**目标**：GPIO / I2C / CAN 三类接口能自主操作，能拿着原理图在 dts 里指认四条链路。
**验收**：CAN 或 RS485 通信成功（**可板内 can0 ↔ can1 对打**）；能说出某外设的 pinctrl / clock / regulator / interrupt 分别对应原理图哪一处。
**投入**：16h

> 本周只保三件：GPIO、I2C、CAN。`⭐` 项时间不够直接砍——BSP 岗要的是「看懂原理图 + 会抓波形」，不是总线数量。

## 任务清单

### 必修

- [ ] GPIO：`libgpiod` 点灯、读按键（`gpiodetect` / `gpioinfo` / `gpioget` / `gpioset`）
- [ ] 设备树里找到 GPIO 控制器节点，理解 `gpio` 属性写法
- [ ] I2C：读一个传感器（`i2cdetect -y <bus>` / `i2cget`），对照 datasheet 寄存器表
- [ ] CAN：`ip link set can0 up type can bitrate 500000`，`candump` / `cansend`
- [ ] **CAN 板内对打**：can0 ↔ can1（120Ω 终端 + 双绞线短接 CANH/CANL），收发都验证
- [ ] 用逻辑分析仪抓一次 I2C 或 CAN 波形，和 datasheet 时序对上
- [ ] 填 [hardware/board.md](../hardware/board.md) 的接口记录与引脚分配表

### ⭐ 可选（不够时间就砍）

- [ ] RS485：串口 + 方向控制引脚（可先两线自环验证方向切换）
- [ ] SPI：读 Flash 或屏幕
- [ ] 网络：MQTT 客户端，往公共 broker 发数据

## 每日记录

<!-- 每天收工前加一节，三行即可：卡在哪 / 怎么解决 / 明天第一步 -->

### 待填 · 待填 h

- 卡在：
- 解决：
- 明天第一步：

## 本周产出

| 类型 | 内容 | 位置 |
| --- | --- | --- |
| 代码 | GPIO 点灯 / I2C 读传感器 / CAN 收发 demo | `src/` |
| 波形 | I2C 或 CAN 截图（PNG，< 1MB） | `docs/img/` |
| 文档 | 引脚分配表 | [hardware/board.md](../hardware/board.md) |

## 复盘（周日）

| 项 | 计划 | 实际 |
| --- | --- | --- |
| 投入小时 | 16 | |
| 必修项完成 | 6/6 | |
| 波形是否抓到 | 是 | |

- 掉队原因：
- 下周调整：

## 面试问答（本周能讲清的 3 个问题）

1. dts 里让一个 I2C 外设工作，需要动哪几个节点？pinctrl、clock、regulator 各在哪配？
2. 「引脚复用冲突」通常长什么样？怎么看出来的？
3. CAN 为什么需要 120Ω 终端电阻？不加会怎样？

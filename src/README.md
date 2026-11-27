自己写的代码放这里，按周或按模块建子目录。

建议结构（第 7 周前会自然长成这样）：

```
src/
├── hello/              # 第 2 周：交叉编译 hello
├── hellomod/           # 第 2 周：第一个内核模块
├── serial-tcp/         # 第 3 周：串口 → TCP 转发
├── fake-host/          # 第 3 周：Python 假上位机（打自己的协议）
├── led-driver/         # 第 5 周：LED 字符设备驱动
├── rpmsg-demo/         # 第 6 周：Linux ↔ M0 双向通信
└── project/            # 第 7 周：项目主体
```

约定：

- 每个子目录自带 `README.md`（编译命令 + 验证方法），10 行就够
- 交叉编译统一用 `CROSS_COMPILE` 变量，不要写死绝对路径
- 内核模块的 Makefile 用 `KDIR ?=` 而不是硬编码路径，换环境才不用改

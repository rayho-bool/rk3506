# 开发环境

> 环境一变就更新这里。第 8 周写 README 的「复现步骤」时，全靠这份文件。

## 主机

| 项 | 值 |
| --- | --- |
| Windows 版本 | 待填（`winver`） |
| CPU / 核数 | 待填 |
| 内存 | 待填 |
| 虚拟化软件 | VMware Workstation（16.2.1 或 17） |

## 虚拟机

| 项 | 值 |
| --- | --- |
| 客户机系统 | Ubuntu **20.04 desktop**（A 盘自带 ISO） |
| 系统盘 / 数据盘 | 60G / 150G（thin） |
| 内存 / vCPU | 待填（建议主机一半 / 4–6） |
| 网络模式 | **桥接**（VM 与板子同网段，省掉端口转发） |
| 3D 加速 | 关闭 |
| 时间同步 | 开启；不用「挂起」，直接关机 |
| IP | 待填（`ip a`） |
| 桌面启动 | 默认 `multi-user.target`，需要时 `sudo systemctl start gdm3` |

## 安装记录

| 日期 | 做了什么 | 命令 / 结果 |
| --- | --- | --- |
| 11/27 | 待填：装 VM | |

## apt 源

20.04 已过标准支持期。若 `apt update` 报 `404` 或 `Release file expired`：

```bash
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
sudo sed -i 's|http://archive.ubuntu.com/ubuntu/|http://old-releases.ubuntu.com/ubuntu/|g; \
             s|http://security.ubuntu.com/ubuntu/|http://old-releases.ubuntu.com/ubuntu/|g' \
  /etc/apt/sources.list
sudo apt update
```

实际做法：

| 日期 | 是否改动 | 结果 |
| --- | --- | --- |
| | | |

## 工具链

| 工具 | 版本 / 来源 | 路径 |
| --- | --- | --- |
| 交叉编译器 | `atk-dlrk3506-toolchain-*`（A 盘 `05、开发工具\03`） | |
| gcc（主机） | | |
| repo | google repo，装在 `~/bin/repo` | |
| make | | |

## 快照

| 快照名 | 时间点 | 内容 |
| --- | --- | --- |
| `snap0-clean` | 装完系统 + 依赖 | 干净可编译环境 |
| `snap1-src` | `repo.sh` 检出完成 | 源码就绪 |

> 环境搞坏了先回滚快照，别修；修一次两小时，回滚两分钟。

## 常用命令

```bash
# ---- 图形界面按需开关 ----
sudo systemctl start gdm3                 # 需要 Qt / LVGL 模拟器时
sudo systemctl isolate multi-user.target  # 用完关掉

# ---- Windows ↔ VM ----
scp -r ./src user@<vm-ip>:~/work/                      # 传到 VM
scp user@<vm-ip>:~/rk3506/rockdev/update.img D:/a_rk3506/out/   # 拉产物去烧写

# ---- VM ↔ 板子 ----
scp hello root@<board-ip>:/tmp/
ssh root@<board-ip>

# ---- 串口（Windows 侧 MobaXterm / PuTTY）----
# 端口：COMx（板载 CH343，装 CH343SER 驱动）  波特率：115200  8N1

# ---- 烧写（Windows 侧）----
# RKDevTool：按住 RECOVERY/升级键上电进 Loader 模式 → 选 update.img → 执行
```

## 已知问题

| 日期 | 现象 | 原因 | 解决 |
| --- | --- | --- | --- |
| | | | |

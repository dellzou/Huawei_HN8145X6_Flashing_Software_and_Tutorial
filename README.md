# 华为 HN8145X6 使能工具包

配套文章：[华为 HN8145X6 使能教程：补全 AllShell、改光模与切华为界面](https://xiaozou123.cn/huawei-hn8145x6-ont-enable-allshell/)

HN8145X6 是 XG-PON 万兆光猫，4GE + 1POTS + 1USB，Wi-Fi 6。这个包解决两件事：把 Telnet 和 AllShell 补上，以及把 boardinfo 改成自己能用的样子。

## 使用顺序

1. `ONT_V500R19C00.exe` → 选“升级” → 选 `echo20_Telnet_Shell.bin` → 启动。灯全亮、连闪、全灭后断电重启。
2. telnet 进 192.168.1.1（root / adminHW），取回 `hw_boardinfo` 和 `hw_boardinfo.bak`。
3. 设备上执行 `decrypt_boardinfo` 解出明文，用 `HW_Dollar2.exe` 改完，V5 保存。
4. 超密在 `hw_ctree.xml` 里，用 `Huawei_Config_Crypto.exe` 解 XML，再解 `$2` 密文。

## 文件

| 文件 | 字节 | SHA256（前 32 位） |
|---|---|---|
| `HW_Dollar2.exe` | 161,280 | `d3110469d8cccc7ca479105393e047fa…` |
| `Huawei_Config_Crypto.exe` | 1,794,560 | `8f005af234f73a456f5e4a127ed4624c…` |
| `ONT_V500R19C00.exe` | 3,503,060 | `a3dfc3daaf05fbff5b0da523dbb50b07…` |
| `echo20_Telnet_Shell.bin` | 19,012 | `13c48faddf373d7f071070ba76ffc915…` |
| `putty.exe` | 574,976 | `a92c1d668f6d060db06535ad346221d2…` |
| `r21shell.bin` | 17,665 | `a247b6b6095139da2ec8b679a1d85c78…` |
| `tftpd64.exe` | 146,656 | `988292db5e71fa50b090ce2bfe668137…` |

`echo20_Telnet_Shell.bin` 是一体补丁：开 Telnet、放开 23 端口、补全 AllShell。`r21shell.bin` 是备用包，刷不进时换它。

## Release

`HN8145X6_E8C_jffs2.zip` 是改回电信界面要用的地区包，1.49 MB。

原始的整机分区备份和超管 cfg **没有上传**：里面带着上一台设备的 `hw_boardinfo`、`hw_ctree.xml`、SSID 和无线密码，属于别人的设备信息。需要就自己做一份备份。

## 相关仓库

同品牌其它机型，命令体系相近，排障时可以互相参照；每个仓库开头都对应一篇文章：

- [华为 F30 工具包](https://github.com/dellzou/Huawei_F30_Flashing_Software_and_Tutorial)：华为 F30，改 SN、改 MAC、取超密
- [华为 HN8145XR 工具包](https://github.com/dellzou/Huawei_HN8145XR_Flashing_Software_and_Tutorial)：华为 HN8145XR，主猫改公版、从猫组网
- [华为 K662D 工具包](https://github.com/dellzou/Huawei_K662D_Flashing_Software_and_Tutorial)：华为 K662D，从猫改光猫模式
- [华为 V173-50 工具包](https://github.com/dellzou/Huawei_V173-50_Flashing_Software_and_Tutorial)：华为 V173-50，R24 装备包与 OBSCTool 日志
- [华为 V173 工具包](https://github.com/dellzou/Huawei_V173_Flashing_Software_and_Tutorial)：华为 V173 主猫，补全 Shell、改公版、改 boardinfo
- [华为 V175 工具包](https://github.com/dellzou/Huawei_V175_Flashing_Software_and_Tutorial)：华为 V175，R23 固件包开 Telnet

## 注意

- 工具来自维修站和论坛，没有签名，杀软会拦。SHA256 对得上再用。
- 改 boardinfo 前一定先备份主备两个文件，改坏了只有这一条退路。
- 只在自己或客户授权的设备上使用。


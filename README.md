# ASUS-TUF-GAMING-B560M-PLUS-WIFI-10-11-RX6600XT-HACKINTOSH-OPENCORE
# MSI-B560M-MORTAR-10-11-RX6600XT-HACKINTOSH-OPENCORE

## 硬件列表

|项目|名称
|-|-
|CPU0|Intel 10th CORE all
|CPU1|Intel 11th CORE all
|主板1|ASUS TUF GAMING B560M PLUS WIFI
|主板2|MSI MORTAR B560M
|主板3|ASUS H510-B560 均支持（igpu需遍历
|主板4|MSI H510-B560 均支持（igpu需遍历
|内存|corsair DDR4 3200MHz 8Gx2
|显卡|AMD RX/intel uhd630（自行重命名config
|硬盘1|SAMSUNG 980PRO 500GB
|硬盘2|KIOXIA RC10 250GB
|无线网卡1|AX201/200（请看驱动包）
|无线网卡2|FV-T919(BCM94360CD)

### 功能测试

- [x] 板载声卡
- [x] 板载网卡
- [x] 睡眠唤醒
- [x] CPU 变频
- [x] 所有USB端口
- [x] 接力和隔空投送
- [x] 板载蓝牙

[❌] 核显硬件加速

### 必读项目
- 硬盘trim开机慢，请关闭trim，方法：SetApfsTrimTimeout设置为0
- 华硕usb唤醒需要去掉EFI/OC/ACPI/SSDT-GPRW,但是本人测试风扇会唤醒不停，微星貌似没问题
- 10代的各位请把EFI-OC内的config10-egpu/igpu重命名为config食用
- 10代+500系要遍历hdmi才可食用，tuf以及mortar已遍历完成，提取edid注入即可食用（具体请参考b站乌龙蜜桃来一打视频，简介文件也在库里哦~）
- 视频链接：https://www.bilibili.com/video/BV1UW4y1J7J2/
- 遍历后的con值欢迎大家在isues的10代核显分区分享自己的con值哦~

### BIOS设置
#### ASUS-11th

- disable igpu（Otherwise, you will not be able to sleep normally）
- disable Intel Rapid Storage Technology

#### ASUS-10th
- Disabe
- Fast Boot
- VT-d
- CSM
- Intel SGX
- CFG Lock
- Enable
- VT-x (no option in BIOS, it's enabled by default)
- Above 4G decoding
- Hyper-Threading
- EHCI/XHCI Hand-off
- OS type: Windows UEFI Mode (Clear Secure Boot Keys or choose `Other` type)
- DVMT Pre-Allocated(iGPU Memory): 64MB

#### MSI-10th

- Boot -- Fast Boot -> Disabled
- Advanced -- PCH Sorage Configuration -- SATA Mode Selection -> AHCI
- Boot -- CSM(Compatibility Support Module) -> Disabled
- Ai Tweaker -- Ai Overclock Tuner -> XMP
- Advanced -- CPU configuration -- Intel Virtualization Technology -> Disabled
- Advanced -- System Agent (SA) Configuration -- VT-D -> Disabled
- Advanced -- System Agent (SA) Configuration -- Above 4G Decoding -> Disabled
- Advanced -- System Agent (SA) Configuration -- Graphics Configuration -- Primary Display -> CPU Graphics 集成显卡配置1
- Advanced -- System Agent (SA) Configuration -- Graphics Configuration -- iGPU Multi-Monitor -> Disabled 集成显卡配置2
- Advanced -- PCH configruation - IOAPIC 24-119 Entries -> Enabled
- Advanced -- PCH-FW Configuration -- TPM Device Selection -> Discrete TPM
- Advanced -- APM Configuration -- ErP Ready -> Disabled
- Advanced -- Network Stack Configuration -- Network Stack -> Disabled
- Boot -- Secure Boot -- OS Type -- Other OS
最后需要 按键盘上的 F10 键保存退出即可.

#### MSI-11th

- Boot -- Fast Boot -> Disabled
- Advanced -- PCH Sorage Configuration -- SATA Mode Selection -> AHCI
- Boot -- CSM(Compatibility Support Module) -> Disabled
- Ai Tweaker -- Ai Overclock Tuner -> XMP
- Advanced -- CPU configuration -- Intel Virtualization Technology -> Disabled
- Advanced -- System Agent (SA) Configuration -- VT-D -> Disabled
- Advanced -- System Agent (SA) Configuration -- Above 4G Decoding -> Disabled
- Advanced -- System Agent (SA) Configuration -- Graphics Configuration -- Primary Display -> PCIE 独立显卡配置 1
- Advanced -- System Agent (SA) Configuration -- Graphics Configuration -- iGPU Multi-Monitor -> Enabled 独立显卡配置 2
- Advanced -- PCH configruation - IOAPIC 24-119 Entries -> Enabled
- Advanced -- PCH-FW Configuration -- TPM Device Selection -> Discrete TPM
- Advanced -- APM Configuration -- ErP Ready -> Disabled
- Advanced -- Network Stack Configuration -- Network Stack -> Disabled
- Boot -- Secure Boot -- OS Type -- Other OS
最后需要 按键盘上的 F10 键保存退出即可.
### 安装过程
- 准备安装U盘：参考OC官方配置，十分好用：[USB Creation](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/mac-install.html#setting-up-opencore-s-efi-environment)，包含macOS、Windows、Linux的U盘制作。
- (重要)使用OpenCoreConfigurator打开我提供的EFI的OC/config.plist 重新生成SystemSerialNumber/SystemUUID/MLB
- 将当前提供的EFI放入U盘EFI磁盘目录下，表示使用当前EFI进行引导
- 开机配置主板各项配置，以及设置U盘UEFI启动顺序第一
- 插入U盘，选择U盘UEFI启动，进行安装系统
- 安装完成进入系统，成功!

### 系统时差

- Windows下管理员身份运行

```
Reg add HKLM\SYSTEM\CurrentControlSet\Control\TimeZoneInformation /v RealTimeIsUniversal /t REG_DWORD /d 1
```

### 设置默认启动项

- `config.plist`勾上仿冒苹果快捷键`PollAppleHotKey`，在启动选择界面，先选中要启动的项，然后按键盘的 `Ctrl` + `Enter` 进入系统即可

- 也有看到说在 `设置`-`启动磁盘` 可选择默认启动项,修改后重启

### 鸣谢
- https://github.com/OrangJuc/
- 橙汁大佬提供ssdt的修改
- 最好的入门教程：[OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/)
- 中文教程：[Xjn的博客](https://blog.xjn819.com/post/opencore-guide.html)
- 中文文档 & kexts集合下载：[OpenCore中文文档](https://oc.skk.moe/)
- 镜像下载 & 中文教程：[黑果小兵](http://blog.daliansky.net)

# PhonePad Windows Xbox 后台连接程序 0.3 测试版

适用 Windows 10/11 x64。手机使用 PhonePad，通过原有蓝牙 HID 连接；不需要改用 Wi-Fi。

1. 电脑首次运行 PhonePad-Windows-Setup-0.3.exe，安装后台连接程序并启用当前用户登录启动。
2. 首次配置需安装官方 HidHide 驱动：https://github.com/nefarius/HidHide/releases/tag/v1.5.230.0 。后台程序自动添加自身读取权限，并隐藏识别出的 PhonePad 原始手柄，避免游戏同时收到原始和 Xbox 两份输入。首次安装后可能需要重新加载手柄设备或重启电脑。
3. 若电脑没有 ViGEmBus 驱动，安装器会打开官方驱动下载页；按官方安装提示完成首次配置，必要时重启。已有可用驱动无需重装。
4. 以后只需在手机打开 PhonePad 并蓝牙连接电脑。电脑程序在后台自动接收输入并创建 Xbox 手柄，无需打开窗口或点击开始。
5. 手机断连后输入归零，后台等待再次连接。没有新报文 500ms 后发送归零状态，超过 5 秒释放虚拟手柄，重新收到报文后恢复。

程序安装到当前用户 LocalAppData/PhonePad，登录启动项名为 PhonePad，可在 Windows 启动应用中关闭。日志为同目录 bridge.log。

LT/RT 在 XInput 中为独立扳机；当前手机触区仍为按下/松开两档。支持多按键、摇杆与按钮同时输入。未实现震动反馈。

原始 PhonePad HID 只对允许列表中的后台程序可读，虚拟 Xbox 手柄保持可见。程序只为产品名 PhonePad Gamepad 且符合报文格式的手柄添加隐藏规则，不隐藏其他设备。保留已有 HidHide 规则；遇到反向隐藏模式或可能影响其他设备的未启用规则时会记录错误，不擅自覆盖。

此版本已在当前电脑完成手机实际输入到 XInput 的验证：651 个手机报文、787 次 XInput 状态核对一致（包含非零输入）；尚未逐款游戏验收。手机系统必须提供 Android HID Device 服务；蓝牙硬件、系统实现差异仍需实测，不能保证每台手机可用。

ViGEmBus 已停止维护：https://docs.nefarius.at/projects/ViGEm/End-of-Life/ 。当前转换器依赖此驱动，请从上述官方发布页安装。

附带 ViGEmClient.dll 来自官方 NuGet Nefarius.ViGEm.Client 1.21.256 的 x64 资源，遵循附带 MIT 许可证。Windows 程序当前未作代码签名。

开发验证：PhonePadBridge.Check.exe --self-test / --probe-driver / --verify-live。开发源码与诊断工具不包含在独立安装器中。

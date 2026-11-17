# PhonePad Windows Xbox 后台连接程序 0.5 一体安装测试版

适用 Windows 10/11 x64。手机使用 PhonePad，通过原有蓝牙 HID 连接；不需要改用 Wi-Fi。

1. 电脑下载并运行 **PhonePad-Windows-Setup-0.5.exe**。一个文件内置官方 ViGEmBus、HidHide 驱动和后台程序，无需另行下载驱动。
2. 按安装向导操作。安装缺少的驱动时，确认 Windows 管理员授权；已有驱动自动跳过。后台程序和自动启动配置属于当前登录用户。
3. 如果首次安装了驱动，请保存工作并重启电脑一次。安装器不会自动重启，后台程序在重启登录后自动运行。
4. 以后只需在手机打开 PhonePad 并蓝牙连接电脑，自动提供 Xbox 输入并隐藏原始 PhonePad，防止重复响应。
5. 可以在 Windows“安装的应用”中卸载 PhonePad。卸载会撤销本程序记录的设备隐藏规则和登录启动项；两个共享驱动保留，避免影响其他软件。

程序安装到当前用户 LocalAppData/PhonePad，登录启动项名为 PhonePad，可在 Windows 启动应用中关闭。日志为同目录 bridge.log。

LT/RT 在 XInput 中为独立扳机；当前手机触区仍为按下/松开两档。支持多按键、摇杆与按钮同时输入。未实现震动反馈。

原始 PhonePad HID 只对允许列表中的后台程序可读，虚拟 Xbox 手柄保持可见。程序只为产品名 PhonePad Gamepad 且符合报文格式的手柄添加隐藏规则，不隐藏其他设备。保留已有 HidHide 规则；遇到反向隐藏模式或可能影响其他设备的未启用规则时会记录错误，不擅自覆盖。

此版本已在当前电脑完成手机实际输入到 XInput 的验证：651 个手机报文、787 次 XInput 状态核对一致（包含非零输入）；尚未逐款游戏验收。手机系统必须提供 Android HID Device 服务；蓝牙硬件、系统实现差异仍需实测，不能保证每台手机可用。

ViGEmBus 已停止维护：https://docs.nefarius.at/projects/ViGEm/End-of-Life/ 。当前转换器依赖此驱动，请从上述官方发布页安装。

附带 ViGEmClient.dll 来自官方 NuGet Nefarius.ViGEm.Client 1.21.256 的 x64 资源，遵循附带 MIT 许可证。Windows 程序当前未作代码签名。

开发验证：PhonePadBridge.Check.exe --self-test / --probe-driver / --verify-live。开发源码与诊断工具不包含在独立安装器中。

一体安装器已验证签名、嵌入驱动 SHA256、构建和已有驱动机器上的重复安装/自动启动。尚未在缺少两个驱动的全新电脑完成安装验收。

## 出现输入问题时复原
桌面或开始菜单打开“PhonePad 恢复原有输入”，点击“恢复原有输入”。也可以单独下载 PhonePad-Recovery.exe 使用。
工具会停止 PhonePad、取消其自动启动，并撤销它记录的原始手柄隐藏规则。不会重置其他应用的隐藏列表。
两个共享驱动不会自动删除。如果怀疑驱动本身有兼容问题，用工具中的“打开系统卸载列表”单独卸载 HidHide / Nefarius Virtual Gamepad Emulation Bus，然后按系统提示重启；这可能影响其他依赖这些驱动的软件。
恢复工具不是整台电脑的系统还原，不撤销其他软件或此前单独安装的 Game Bar。需要重新启用 PhonePad 时，再运行一体安装包。
已通过编译、启动项归属检查和当前配置只读检查；未在用户当前正常使用的电脑执行破坏性回退实测。

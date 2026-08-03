# SideLinker

SideLinker 是一个为无头 Mac mini 准备的 Sidecar 辅助工具。它解决的核心问题是：当 Mac mini 没有外接显示器时，如何更方便地把 iPad 作为唯一屏幕唤起、连接和管理。

重要说明：无头 Mac mini 使用 iPad 作为唯一屏幕时，SideLinker 需要配合 BetterDisplay 创建并保持虚拟显示器。SideLinker 负责触发、连接和管理流程，BetterDisplay 负责提供无头环境下可用的虚拟屏幕。

它由 Mac 端菜单栏应用和 iPad 端应用组成。Mac 端负责发现 iPad、建立随航连接、提供局域网控制接口和蓝牙信标；iPad 端负责发起唤醒、查看状态、完成配对，并在需要时触发连接或断开。

## 下载

- Mac 端最新版：前往 [GitHub Releases](https://github.com/wberry9813/SideLinker-Home/releases) 下载。
- iPad 端：前往 [App Store](https://apps.apple.com/app/sidelinker/id6760007015) 安装。
- 完整图文教程：查看 [飞书文档](https://vcn1p70mh4sm.feishu.cn/wiki/X6CYwbIjgiivxUkjbLdc1Z5AnPd)。

建议 Mac 端和 iPad 端都保持最新版本。当前推荐 Mac 端版本为 `v1.0.5`。

## 适用场景

SideLinker 最适合这些场景：

- 你有一台无头 Mac mini，没有长期连接显示器。
- 你希望用 iPad 作为 Mac mini 的主要或唯一屏幕。
- 你不想每次都接显示器、键盘、鼠标，只为了打开 Sidecar。
- 你希望从 iPad 上一键唤起 Mac 端随航连接。
- 你希望 iPad 靠近 Mac 时自动连接，离开后自动断开。
- 你希望通过 USB、局域网、蓝牙近场等多种方式提高连接成功率。
- 你愿意配合 BetterDisplay 使用虚拟屏幕，让无头 Mac mini 在没有实体显示器时也有可用显示输出。

SideLinker 不是 Apple Sidecar 的替代品。它是一个辅助工具，用来更方便地触发和管理 macOS 自带的 Sidecar 能力。

## 使用前准备

开始前请确认：

- Mac 和 iPad 都支持 Apple Sidecar。
- Mac 与 iPad 登录了同一个 Apple ID，或至少系统 Sidecar 本身可以正常连接。
- 两台设备已开启蓝牙。
- 如果使用无线连接，两台设备建议处于同一 Wi-Fi 网络。
- 如果使用 USB 连接，请使用稳定的数据线，并在 iPad 上完成“信任此电脑”。
- iPad 端首次启动时，请允许蓝牙、局域网和通知权限。
- Mac 端首次启动时，请允许必要的网络和蓝牙访问。
- 如果 Mac mini 是无头使用，请先安装并配置 BetterDisplay 虚拟屏幕。

如果系统自带 Sidecar 无法手动连接，SideLinker 也无法绕过系统限制强行连接。

## Mac 端安装

1. 打开 [GitHub Releases](https://github.com/wberry9813/SideLinker-Home/releases)，下载最新的 SideLinker Mac 安装包。
2. 将 SideLinker 拖入 `Applications` 文件夹。
3. 首次打开时，如果 macOS 提示安全限制，请在系统设置中允许打开。
4. 启动后确认菜单栏出现 SideLinker 图标。
5. 点击菜单栏图标，进入设置页。
6. 建议开启开机自启，这样 Mac mini 重启后也能自动等待 iPad 连接。

Mac 端启动后会做几件事：

- 在菜单栏显示连接状态。
- 发布局域网服务，供 iPad 发现和控制。
- 发布蓝牙信标，供 iPad 近场识别。
- 监听 iPad 发来的连接或断开请求。
- 将 Mac 端随航状态同步给 iPad。

## iPad 端安装

1. 在 iPad 上打开 [App Store 页面](https://apps.apple.com/app/sidelinker/id6760007015)。
2. 安装 SideLinker。
3. 首次启动后，允许蓝牙、局域网和通知权限。
4. 保持 iPad 与 Mac 在同一 Wi-Fi，或用 USB 数据线连接。
5. 打开主界面，查看 Mac 是否在线。

如果 iPad 端提示需要更新 Mac 端，请点击提示跳转到 GitHub Releases 下载最新版 Mac 应用。

## 首次配对

推荐使用二维码配对：

1. 在 Mac 端点击菜单栏 SideLinker 图标。
2. 点击二维码按钮，显示 Mac 端配对二维码。
3. 在 iPad 端进入配对或设置页面。
4. 扫描 Mac 端二维码。
5. iPad 会保存 Mac 的局域网地址、端口和控制令牌。

配对完成后，iPad 可以通过局域网直接向 Mac 发送连接、断开和状态查询请求。SideLinker 也会通过 Bonjour 自动发现 Mac，减少手动填写地址的需要。

## 连接方式

### iPad 一键连接

在 iPad 主界面滑动连接控件，SideLinker 会优先尝试可用通道：

- 局域网 Web API
- 蓝牙物理指令
- iCloud 状态同步
- USB 连接状态辅助判断

如果 Mac 端在线并且系统 Sidecar 可用，Mac 会开始连接 iPad。

### Mac 菜单栏连接

在 Mac 端点击菜单栏 SideLinker 图标，可以手动触发连接或断开。这个方式适合 Mac 仍接着临时显示器时做首次测试。

### USB 一插即连

将 iPad 通过数据线连接到 Mac 后，Mac 端会检测 USB 设备事件，并尝试优先连接刚插入的 iPad。

如果没有触发，请检查：

- 数据线是否支持数据传输。
- iPad 是否已解锁。
- iPad 是否已信任这台 Mac。
- macOS Finder 是否能看到这台 iPad。

### 蓝牙近场连接

开启 Pro 近场功能后，iPad 靠近 Mac 时会广播近场信号，Mac 端检测到足够近的 RSSI 后可自动触发随航连接。

这个功能适合无头 Mac mini：你只需要拿着 iPad 靠近 Mac，Mac 就能尝试把 iPad 变成屏幕。

### 自动断开

开启自动断开后，iPad 远离 Mac 一段时间后，SideLinker 会尝试断开随航，避免 Mac 长时间保持无用连接。

## Pro 功能

SideLinker Pro 当前包含这些增强能力：

- 近场感应自动连接。
- iPad 远离后自动断开。
- 随航状态通知。
- Lock Screen / Dynamic Island Live Activity 状态显示。
- 远程开关 SideLinker-HD 虚拟屏幕。
- Pro 权益通过 iCloud 同步到 Mac 端。

Pro 购买在 iPad 端完成。购买或恢复后，Mac 端会通过 iCloud 自动获得授权状态。

## BetterDisplay 与虚拟屏幕

SideLinker 的无头 Mac mini 使用场景必须配合 BetterDisplay。SideLinker 可以帮助创建和管理虚拟屏幕，例如 `SideLinker-HD`，但虚拟显示能力由 BetterDisplay 提供。

适用场景：

- 无头 Mac mini 没有物理显示器。
- 你希望 Mac 在没有显示器时仍保持合适的分辨率。
- 你希望随航连接后镜像到指定虚拟屏幕。

在 Mac 端设置中可以检查 BetterDisplay 状态、安装或打开 BetterDisplay，并创建虚拟屏幕。如果虚拟屏幕创建失败，请确认：

- BetterDisplay 已安装并正在运行。
- BetterDisplay HTTP API 已开启。
- BetterDisplay 版本支持虚拟屏幕能力。
- 某些虚拟屏幕能力可能需要 BetterDisplay Pro。

## 常见问题

### iPad 找不到 Mac

请按顺序检查：

1. Mac 端 SideLinker 是否正在运行。
2. iPad 和 Mac 是否在同一 Wi-Fi。
3. iPad 是否允许 SideLinker 使用局域网。
4. Mac 防火墙是否阻止了 SideLinker。
5. Mac 菜单栏设置中的 Web API 是否开启。
6. 尝试用二维码重新配对。

### 点击连接后很快断开

SideLinker 使用 macOS 系统 Sidecar 能力。如果系统 Sidecar 自身连接不稳定，SideLinker 也会表现为连接后马上断开。

建议先测试：

1. 在 macOS 控制中心手动连接 iPad。
2. 确认 iPad 屏幕已点亮并解锁。
3. 确认两端蓝牙和 Wi-Fi 正常。
4. 尝试 USB 连接。
5. 重启 Mac 和 iPad 后再试。

### 蓝牙能发现，但连接失败

请检查：

- 两端蓝牙是否开启。
- iPad 是否距离 Mac 足够近。
- iPad 是否开启了 SideLinker 的蓝牙权限。
- Mac 端是否是最新版。
- 尝试先用二维码配对，再使用蓝牙近场连接。

### USB 插入没有反应

请检查：

- 线缆是否支持数据传输。
- iPad 是否已解锁。
- 是否出现“信任此电脑”提示。
- Finder 是否能识别 iPad。
- 重新插拔后等待几秒。

### Pro 状态没有同步到 Mac

请检查：

- iPad 和 Mac 是否登录同一个 Apple ID。
- iCloud Drive 或 iCloud 是否可用。
- 网络是否正常。
- 在 iPad 端尝试恢复购买。
- 在 Mac 端重新打开 SideLinker。

## 权限说明

SideLinker 使用这些权限来完成连接：

- 蓝牙：用于近场发现、信标广播和物理连接指令。
- 局域网：用于 iPad 与 Mac 之间的本地控制请求。
- iCloud：用于同步配对信息、连接状态和 Pro 权益。
- 通知：用于提醒随航连接状态变化。

SideLinker 不读取屏幕内容，不上传用户文件，不采集浏览记录。

## 导出日志与反馈

如果遇到连接问题，请同时导出 Mac 端和 iPad 端日志，并附上：

- Mac 型号和 macOS 版本。
- iPad 型号和 iPadOS 版本。
- SideLinker Mac 版本。
- SideLinker iPad 版本。
- 使用的连接方式：无线、USB、蓝牙近场或手动连接。
- 问题发生的大概时间。

这样可以更快判断问题出在系统 Sidecar、局域网发现、蓝牙链路、iCloud 同步还是 SideLinker 状态机。

## 法律与隐私

- [Privacy Policy](docs/privacy.html)
- [隐私政策](docs/privacy-zh.html)
- [Terms of Service](docs/terms.html)
- [服务条款](docs/terms-zh.html)

# Android综合工具箱

在 Windows 上签名 APK、打渠道包、加固、查看 APK 信息，以及生成增量包。

安装包在 [Releases](https://gitee.com/dlkw/android-tools-releases/releases) 的附件中。请从那里下载 exe，不要从仓库文件列表里找安装包。

## 下载与运行

1. 打开 [Releases](https://gitee.com/dlkw/android-tools-releases/releases)，进入要安装的版本。
2. 下载该版本附件中的 exe，文件名形如 `Android综合工具箱-1.0.2.exe`。
3. 需要核对文件时，用该版本说明里的 SHA256。PowerShell：

```powershell
Get-FileHash -Algorithm SHA256 ".\Android综合工具箱-1.0.2.exe"
```

4. 单独建一个文件夹，把 exe 放进去再双击启动。首次运行会在同目录生成 `configs.json`（签名配置、SDK 路径等）。换目录使用时把这个文件一并拷走。
5. 若本机没有可用的 .NET 桌面运行时，程序会提示并打开下载页面。安装完成后再打开即可。
6. 启动后如果发布页有更高版本，程序会提示并打开 [Releases](https://gitee.com/dlkw/android-tools-releases/releases)。

安装包不包含 .NET 运行时，需要单独安装 **.NET 8 或更高版本的桌面运行时（x64）**。

## 使用前准备

| 项目 | 要求 |
| --- | --- |
| 系统 | Windows 10 版本 1607（x64）及以上，或 Windows 11 |
| 运行时 | [.NET 8 桌面运行时（x64）](https://dotnet.microsoft.com/zh-cn/download/dotnet/8.0) 或更高版本。安装「桌面运行时 / Desktop Runtime」 |
| 首页 | [Microsoft Edge WebView2 运行时](https://developer.microsoft.com/microsoft-edge/webview2/)。未安装时首页会提示，其余功能仍可使用 |
| 渠道打包、APK 加固 | 本机 JDK 8 或更高版本，以及 Android SDK。启动后若未配置 SDK，按提示到「设置」里填写 |
| 签名、渠道打包、加固 | 在「签名配置」中至少添加一套密钥库 |

各功能的结果都写到所选输出目录，原始 APK 不会被修改。

## 程序能做什么

- 批量签名。输出 `原文件名_signed.apk`
- 多渠道打包。渠道文件每行一条：`渠道代码|渠道名称`
- APK 加固。未签名为 `原文件名_jiagu.apk`，签名后为 `原文件名_jiagu_sign.apk`
- 应用图标生成
- 增量包
- 查看 APK 的包名、版本和签名信息
- 在「设置」中配置 SDK、JDK，以及清除本程序产生的临时缓存

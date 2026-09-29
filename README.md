# Android综合工具箱 · 发布仓库

本仓库只存放 **Android综合工具箱** 的 Windows 发行包。

源码、问题反馈和完整功能说明在源码仓库：<https://gitee.com/dlkw/android-tools>

Gitee 仓库首页默认展示根目录的 `README.md`。若希望打开本仓库就能看到这份说明，将本文件复制或改名为 `README.md` 即可。

## 下载与运行

1. 进入对应版本目录（例如 `v1.0.0/`）。
2. 下载 `Android综合工具箱.exe`。
3. 用同目录的 `SHA256SUMS.txt` 核对文件。PowerShell：

```powershell
Get-FileHash -Algorithm SHA256 ".\Android综合工具箱.exe"
```

把输出的哈希与 `SHA256SUMS.txt` 中的值比对，一致后再运行。

4. 单独建一个文件夹，把 exe 放进去再双击启动。程序是绿色软件，首次运行会在 exe 同目录生成 `configs.json`（签名配置、SDK 路径等）。换目录使用时把这个文件一并拷走。

发行包是 **Windows x64、自包含 .NET 8 的单个 exe**，不需要再安装 .NET 运行时。

## 使用前准备

| 项目 | 要求 |
| --- | --- |
| 系统 | Windows 10 版本 1607（x64）及以上，或 Windows 11 |
| 首页 | [Microsoft Edge WebView2 Runtime](https://developer.microsoft.com/microsoft-edge/webview2/)。未安装时首页会提示，其余功能仍可使用 |
| 渠道打包、APK 加固 | 本机 JDK 8 或更高版本，以及 Android SDK。启动后若未配置 SDK，按提示到「设置」里填写 |
| 签名、渠道打包、加固 | 在「签名配置」中至少添加一套密钥库 |

原始 APK 不会被修改，各功能的结果都写到所选输出目录。

## 程序能做什么

- 批量签名
- 多渠道打包
- APK 加固（ATB Shield，以及百度加固方案）
- 应用图标生成（各密度与自适应图标）
- 增量包
- APK 信息查看
- 签名配置与 SDK 路径设置

各功能的操作步骤以源码仓库 `README.md` 为准。

## 目录约定

```
releases.readme.md
v1.0.0/
  Android综合工具箱.exe
  SHA256SUMS.txt
v1.1.0/
  Android综合工具箱.exe
  SHA256SUMS.txt
```

- 版本目录使用 `v主版本.次版本.修订号`。
- 每个版本目录只放一份 exe 和对应的 `SHA256SUMS.txt`。
- 不要提交 `configs.json`、密钥库（`.jks` / `.keystore`）或任何密码。

`SHA256SUMS.txt` 每行格式：

```
<64位大写或小写十六进制>  Android综合工具箱.exe
```

## 版本记录

| 版本 | 日期 | 说明 |
| --- | --- | --- |
| — | — | 尚未发布。首次放入安装包后在此补一行 |

## 维护者：发布新版本

在源码仓库打包：

```bat
publish.bat
```

或：

```bat
npm run build
```

成功后产物为源码仓库下的 `publish\Android综合工具箱.exe`。

然后在本仓库：

1. 新建目录 `vX.Y.Z/`，把该 exe 拷入，文件名保持 `Android综合工具箱.exe`。
2. 在该目录生成校验文件：

```powershell
Get-FileHash -Algorithm SHA256 ".\Android综合工具箱.exe" |
  ForEach-Object { "{0}  {1}" -f $_.Hash.ToLower(), "Android综合工具箱.exe" } |
  Set-Content -Encoding ascii SHA256SUMS.txt
```

3. 在上面的「版本记录」补上版本、日期和变更摘要。
4. 提交并推送到 <https://gitee.com/dlkw/android-tools-releases>。

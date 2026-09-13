# GitHub 发布准备清单

[返回 README](../README.md) · [许可说明](许可说明.md) · [v0.9.3 更新说明](RELEASE_NOTES_v0.9.3.md)

作者：Mike Wu。v0.9.3 公开内容为免费 Windows 程序及使用资料；WB Studio 项目源码、测试工程和构建工程暂不公开。程序采用 **PolyForm Strict License 1.0.0**。

## 上传到仓库根目录的内容

将发布材料中的 `repository` 文件夹内容上传到 GitHub 仓库根目录。上传后应直接看到 `README.md`、`LICENSE`、`NOTICE`、`CITATION.cff`、`docs` 和 `.github`，不要多套一层 `repository` 文件夹。

仓库只包含软件介绍、使用指南、许可证、第三方说明、截图、问题模板和版本说明。不要上传项目工作目录、`src`、`tests`、`build`、`data`、运行日志或原始实验图片。

## Release 附件

将 `release-assets` 文件夹中的两个文件添加到 GitHub Release `v0.9.3`：

- `WB_Studio_v0.9.3_Windows_x64.zip`：Windows 10/11 x64 便携程序，普通使用者下载这一项。
- `SHA256SUMS.txt`：安装包 SHA-256 校验值。

本次不上传 WB Studio 源码，也不上传 Java、Python 或构建依赖的源码归档。程序包内保留运行所需的第三方组件许可和声明文件。

## 建议的 Release 信息

- 标签：`v0.9.3`
- 标题：`WB Studio v0.9.3（Windows 测试版）`
- 勾选 **Pre-release**，因为这是测试版。
- Release 正文可直接复制发布材料目录中的 `RELEASE_BODY.md`。

GitHub 创建仓库时，许可证模板选择 **None / 不添加许可证**，然后上传材料中已有的 `LICENSE`。不要再添加 MIT、GPL 或 Apache 等冲突许可证。

## 发布前检查

1. 确认仓库中没有 `data`、`.sqlite`、原始图片、日志或个人路径。
2. 下载 Release 附件并用 `SHA256SUMS.txt` 核对哈希。
3. 将 ZIP 完整解压到新的本地目录，启动 `WB Studio.exe`。
4. 点击“自带测试示例”，完成一次测量、比值统计和 PDF 导出。
5. 在另一台 Windows 电脑上验证时，记录 WebView2 Runtime、系统版本和启动结果。

GitHub 自动生成的 Source code ZIP 只是文档仓库快照，不包含 WB Studio 实现源码，也不是可运行程序。收费、商业和机构使用范围以仓库内英文 `LICENSE` 为准。

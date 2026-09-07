# Third-party corresponding source / 第三方对应源码

WB Studio 自有开发源码暂不提供。第三方组件的源码材料与 WB Studio 项目源码分别处理。

## Eclipse Temurin / OpenJDK

程序随附未修改 OpenJDK 源码生成的 Eclipse Temurin 21.0.12.1+1 精简 Java 运行时，适用 GPL v2 with Classpath Exception 及随附第三方许可。

同一次 GitHub Release 应同时上传以下完整上游源码附件，供下载者免费获取：

`OpenJDK21U-jdk-sources_21.0.12.1_1.tar.gz`

本次已下载该文件并与发布者 SHA-256 校验结果核对。具体校验值在 Release 附件 `SHA256SUMS.txt` 中。

- [对应版本上游源码](https://github.com/adoptium/temurin21-binaries/releases/download/jdk-21.0.12.1%2B1/OpenJDK21U-jdk-sources_21.0.12.1_1.tar.gz)
- [上游 SHA-256](https://github.com/adoptium/temurin21-binaries/releases/download/jdk-21.0.12.1%2B1/OpenJDK21U-jdk-sources_21.0.12.1_1.tar.gz.sha256.txt)
- [上游发布页](https://github.com/adoptium/temurin21-binaries/releases/tag/jdk-21.0.12.1%2B1)

Java 运行时通过上游 JDK 自带 jlink 生成，未修改上游源码。使用的参数：

```text
jlink --add-modules java.base,java.compiler,java.desktop,java.rmi,java.scripting --strip-debug --no-header-files --no-man-pages --compress=zip-6 --output runtime
```

精确模块与运行文件校验见 [引擎清单](docs/imagej-manifest.json)。许可证保存在程序的 `app/imagej/runtime/legal`；程序完整源文件的获取渠道应随二进制下载持续提供。

## ImageJ 与其他组件

- ImageJ 1.54q 为公共领域软件，保留上游免责声明：[版本源码](https://github.com/imagej/ImageJ/tree/v1.54q)。
- Python、NumPy、Pillow、ReportLab、charset-normalizer 与 WebView2 等依赖的版本、来源及许可位置见 [第三方组件说明](docs/第三方组件说明.md)。程序保留其随附许可元数据和必要声明。

这里的 Java 源码附件仅用于第三方再分发材料，不是 WB Studio 软件的开发工程。

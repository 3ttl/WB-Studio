# WB Studio ImageJ engine

This directory is a self-contained Windows x64 runtime. It contains actual
ImageJ 1.54q, a WB Studio Java IPC bridge, and a reduced Eclipse Temurin OpenJDK
runtime. ImageJ is not installed globally, and Fiji is not required.

## ImageJ 1.54q

- Publisher download: https://wsr.imagej.net/download/jars/ij.jar
- Versioned upstream source: https://github.com/imagej/ImageJ/tree/v1.54q
- Upstream source archive: https://github.com/imagej/ImageJ/archive/refs/tags/v1.54q.zip
- SHA-256 of the bundled `ij.jar`: `b61b298ad7540309553e81eb0a769bd26267c77adbfe732be5ca51c7ff7257b6`
- License: public domain; the unmodified upstream disclaimer is included as
  `LICENSE-ImageJ.txt`. Source: https://imagej.net/ij/disclaimer.html

The publisher's unversioned jar URL can change. Reproducing this engine requires
the recorded 1.54q artifact and SHA-256, not an arbitrary newer download.

## Eclipse Temurin 21.0.12.1+1

- Publisher release: https://github.com/adoptium/temurin21-binaries/releases/tag/jdk-21.0.12.1%2B1
- Original Windows x64 JDK: https://github.com/adoptium/temurin21-binaries/releases/download/jdk-21.0.12.1%2B1/OpenJDK21U-jdk_x64_windows_hotspot_21.0.12.1_1.zip
- JDK SHA-256: `f9d6e191ab098c0d416e7d588a24420a8621cd2f4720dab2459b8b7b2d2d8b4e`
- Corresponding complete upstream sources: https://github.com/adoptium/temurin21-binaries/releases/download/jdk-21.0.12.1%2B1/OpenJDK21U-jdk-sources_21.0.12.1_1.tar.gz
- Source checksum: https://github.com/adoptium/temurin21-binaries/releases/download/jdk-21.0.12.1%2B1/OpenJDK21U-jdk-sources_21.0.12.1_1.tar.gz.sha256.txt
- Licenses: GPL v2 with Classpath Exception and the applicable bundled third
  party licenses, preserved under `runtime/legal/`; the upstream notice is
  included in `NOTICE-Temurin.txt`.

The runtime was produced without modifying OpenJDK source, using its `jlink`:

```text
jlink --add-modules java.base,java.compiler,java.desktop,java.rmi,java.scripting --strip-debug --no-header-files --no-man-pages --compress=zip-6 --output src/imagej/runtime
```

These modules cover ImageJ's dependencies reported by `jdeps`; transitive Java
modules are included automatically. The resulting runtime is approximately
46.7 MiB. The development JDK and download archive remain under
`build/imagej-toolchain/` and are not part of the program distribution.

## WB Studio bridge

The program includes the compiled WB Studio IPC adapter and does not include its development source. ImageJ measurement logic remains in the unchanged upstream JAR. The private Java process is reused for measurements and closes with the program.

## Quantification boundary

- Input is an unsigned 8/16-bit raw pixel array. No source pathname is sent to
  Java and the engine cannot overwrite the source image.
- Scaled 16-to-8 analysis executes `ShortProcessor.setMinAndMax` followed by
  `TypeConverter.convertToByte(true)`. Eight-bit source pixels remain unchanged.
- Native analysis retains original integer intensity. Display contrast, gamma,
  inverted LUT and preview bytes are never passed to this engine.
- Rotation executes the actual `ImageProcessor.rotate` implementation with
  explicit nearest/bilinear interpolation, clockwise angle, zero fill and no
  expansion. Zero degrees is an explicit no-op: ImageJ's `ShortProcessor`
  otherwise resamples edge pixels even for a call to `rotate(0)`.
- Statistics execute `ImageStatistics.getStatistics` on integer rectangular
  ROIs with no threshold or calibration. Area/mean/min/max come from ImageJ;
  raw integrated density uses a Java `long` weighted sum of ImageJ's exact raw
  histogram (256 or 65536 levels), avoiding mean-times-area rounding.
- WB Studio defines ROI selection, lane matching, and local top/bottom
  background subtraction. Those workflow choices are not claimed to be
  ImageJ's gel-analysis peak-area algorithm or a journal certification.


The complete matching Java upstream sources accompany this release as a separate archive. See UPSTREAM_SOURCES.md in the program root.

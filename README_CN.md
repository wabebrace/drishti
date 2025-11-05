# Drishti 快速入门 (中文)

[English](README.rst) | 简体中文

## 什么是 Drishti？

Drishti 是一个实时眼睛追踪和人脸检测的 C++11 库，专为嵌入式和移动设备设计。

## 主要特性

✨ **实时处理**: 在移动设备上实现 30 FPS 的眼睛追踪  
👁️ **眼睛追踪**: 精确的虹膜和瞳孔检测  
📱 **跨平台**: 支持 iOS, Android 和桌面系统  
🚀 **轻量级**: SDK 小于 1 MB，模型资源小于 4 MB  
⚡ **GPU 加速**: 使用 OpenGL ES 2.0/3.0 优化  

## Android Studio 开发指南

想在本地使用 Android Studio 开发此项目？请参考完整的中文指南：

📖 **[Android Studio 本地开发指南](ANDROID_STUDIO_SETUP_CN.md)**

这份指南包含:
- ✅ 完整的系统要求和环境准备
- ✅ 详细的项目配置步骤
- ✅ 多种构建方法 (GUI 和命令行)
- ✅ 常见问题解决方案
- ✅ 项目结构说明

## 快速开始

### 1. 准备环境

安装必需软件:
- Android Studio 3.2.1+
- CMake 3.9.2+
- Android NDK r17c 或 r18b (重要: 不支持 r19+)

### 2. 克隆仓库

```bash
git clone --recursive https://github.com/elucideye/drishti
cd drishti
```

### 3. 配置项目

创建 `android-studio/local.properties` 文件:

```properties
sdk.dir=/path/to/Android/Sdk
ndk.dir=/path/to/Android/Sdk/ndk/r18b
cmake.dir=/usr/local
```

参考示例文件: `android-studio/local.properties.example`

### 4. 打开项目

在 Android Studio 中打开 `drishti/android-studio` 目录，等待 Gradle 同步完成。

### 5. 运行应用

连接 Android 设备，点击 Run 按钮或按 `Shift + F10`。

## 项目结构

```
drishti/
├── android-studio/                    # Android Studio 主项目
├── src/examples/facefilter/          # Face Filter 示例应用
│   └── android-studio/               # 可独立运行的示例
├── ANDROID_STUDIO_SETUP_CN.md        # 详细中文开发指南 ⭐
├── README_CN.md                       # 本文件
└── README.rst                         # 英文 README
```

## 示例应用

### Face Filter (人脸滤镜)

- **位置**: `src/examples/facefilter/android-studio/`
- **功能**: 实时人脸检测、眼睛追踪、OpenGL 渲染
- **最低要求**: Android 7.0 (API 24)

### 构建示例

```bash
cd src/examples/facefilter/android-studio
./gradlew assembleDebug
```

## 技术规格

| 项目 | 说明 |
|------|------|
| **语言** | C++11, Java |
| **图形 API** | OpenGL ES 2.0/3.0 |
| **构建系统** | CMake + Gradle |
| **包管理** | Hunter |
| **平台** | Android, iOS, Linux, macOS, Windows |
| **最小 Android 版本** | API 24 (Android 7.0) |

## 支持的架构

- `arm64-v8a` (64位 ARM - 推荐)
- `armeabi-v7a` (32位 ARM)
- `x86_64` (模拟器)

## 常见问题

### 1. NDK 版本问题

❌ **问题**: NDK r19+ 不被支持  
✅ **解决**: 使用 NDK r17c 或 r18b

### 2. 首次构建很慢

❌ **问题**: Hunter 下载依赖需要很长时间  
✅ **正常**: 首次构建可能需要 20-60 分钟，后续会使用缓存

### 3. Gradle 同步失败

❌ **问题**: Failed to sync Gradle project  
✅ **解决**: 检查 `local.properties` 路径是否正确

更多问题请查看 [详细中文指南](ANDROID_STUDIO_SETUP_CN.md#常见问题)

## 资源链接

- 📘 [详细中文开发指南](ANDROID_STUDIO_SETUP_CN.md) - 完整的设置和开发文档
- 📄 [英文 README](README.rst) - 原始项目文档
- 🔧 [Face Filter README](src/examples/facefilter/android-studio/README.md) - 示例应用文档
- 🌐 [Hunter 文档](https://docs.hunter.sh/) - 包管理器文档
- 📚 [Android NDK](https://developer.android.com/ndk) - NDK 官方文档

## 示例配置文件

项目提供了示例配置文件，方便快速开始:

- `android-studio/local.properties.example` - 主项目配置示例
- `src/examples/facefilter/android-studio/local.properties.example` - Face Filter 配置示例

复制这些文件到 `local.properties` 并根据你的系统修改路径。

## 应用功能演示

Face Filter 应用展示了以下功能:

- 🎯 **实时人脸检测**: 从视频流中检测人脸
- 👀 **眼睛追踪**: 追踪眼睛位置、虹膜和瞳孔
- 📐 **特征点检测**: 检测 64 个面部特征点
- 🎨 **实时渲染**: 使用 OpenGL ES 高效渲染
- 📷 **Camera2 API**: 使用现代 Android 相机 API

## 系统要求总结

### 软件
- ✅ Android Studio 3.2.1+
- ✅ CMake 3.9.2+
- ✅ Android NDK r17c/r18b
- ✅ Ninja 构建系统
- ✅ Android SDK API 24+

### 硬件
- ✅ Android 设备或模拟器
- ✅ 摄像头支持
- ✅ 4GB+ RAM
- ✅ 10GB+ 磁盘空间

## 构建命令速查

```bash
# 调试版本
./gradlew assembleDebug

# 发布版本
./gradlew assembleRelease

# 指定架构
./gradlew assembleDebug -Parch=arm64-v8a

# 安装到设备
./gradlew installDebug

# 清理
./gradlew clean
```

## 贡献

欢迎提交 Issue 和 Pull Request！

## 许可证

BSD 3-Clause License

---

**需要帮助？** 请查看 [详细中文开发指南](ANDROID_STUDIO_SETUP_CN.md)

**更多信息**: 参考 [英文 README](README.rst) 获取完整的技术文档

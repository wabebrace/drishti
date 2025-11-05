# Drishti Android Studio 本地开发指南

本文档详细说明如何在本地使用 Android Studio 开发 Drishti 项目。

## 目录

- [系统要求](#系统要求)
- [环境准备](#环境准备)
- [项目配置](#项目配置)
- [构建项目](#构建项目)
- [常见问题](#常见问题)
- [项目结构](#项目结构)

## 系统要求

### 必需软件

1. **Android Studio** 3.2.1 或更高版本
   - 下载地址: https://developer.android.com/studio
   
2. **CMake** 3.9.2 或更高版本
   - macOS: `brew install cmake`
   - Linux: `sudo apt-get install cmake` 或从官网下载
   - Windows: 从 https://cmake.org/download/ 下载安装包
   
3. **Android NDK** r17c 或 r18b
   - **重要**: 当前不支持 NDK r19 及更高版本
   - 可以在 Android Studio 的 SDK Manager 中下载旧版本 NDK
   - 或者从 https://developer.android.com/ndk/downloads/older_releases 下载
   
4. **Ninja** 构建系统
   - 通常随 CMake 或 Android Studio 一起安装
   
5. **Android SDK** API Level 24 (Android 7.0) 或更高
   - 在 Android Studio 的 SDK Manager 中安装

### 硬件要求

- 支持 USB 调试的 Android 设备 (推荐)，或者 Android 模拟器
- 设备需要有摄像头和自动对焦功能
- 至少 4GB RAM (8GB 推荐)
- 至少 10GB 可用磁盘空间

## 环境准备

### 1. 克隆仓库

```bash
# 克隆项目及其子模块
git clone --recursive https://github.com/elucideye/drishti
cd drishti
```

或者先克隆再初始化子模块:

```bash
git clone https://github.com/elucideye/drishti
cd drishti
git submodule update --init --recursive
```

### 2. 安装 Android Studio

1. 下载并安装 Android Studio
2. 首次启动时完成安装向导
3. 安装推荐的 SDK 组件

### 3. 配置 Android SDK 和 NDK

在 Android Studio 中:

1. 打开 **Tools → SDK Manager**
2. 在 **SDK Platforms** 标签页:
   - 安装 **Android 7.0 (API Level 24)** 或更高版本
   - 安装 **Android 8.1 (API Level 27)** (推荐)
   
3. 在 **SDK Tools** 标签页:
   - 安装 **Android SDK Build-Tools**
   - 安装 **NDK (Side by side)** - 选择 r17c 或 r18b 版本
   - 安装 **CMake**

### 4. 安装 CMake 3.9.2+

#### macOS
```bash
brew install cmake
```

#### Ubuntu/Debian
```bash
sudo apt-get update
sudo apt-get install cmake
```

#### Windows
从 https://cmake.org/download/ 下载并安装最新版本。

验证安装:
```bash
cmake --version
```

应该显示 3.9.2 或更高版本。

## 项目配置

### 1. 创建 local.properties 文件

在项目的 `android-studio` 目录下创建 `local.properties` 文件。有两个 Android Studio 项目:

#### 主项目: `drishti/android-studio/`

创建文件 `drishti/android-studio/local.properties`:

```properties
# Android SDK 路径
sdk.dir=/Users/你的用户名/Library/Android/sdk

# Android NDK 路径 (使用 r17c 或 r18b)
ndk.dir=/Users/你的用户名/Library/Android/sdk/ndk/r18b

# CMake 路径
cmake.dir=/usr/local
```

#### 示例项目: `drishti/src/examples/facefilter/android-studio/`

创建文件 `drishti/src/examples/facefilter/android-studio/local.properties`:

```properties
# Android SDK 路径
sdk.dir=/Users/你的用户名/Library/Android/sdk

# Android NDK 路径 (使用 r17c 或 r18b)  
ndk.dir=/Users/你的用户名/Library/Android/sdk/ndk/r18b

# CMake 路径
cmake.dir=/usr/local
```

**路径说明:**

- **macOS**: 
  - SDK: `/Users/用户名/Library/Android/sdk`
  - CMake: `/usr/local` (通过 Homebrew 安装)
  
- **Linux**:
  - SDK: `/home/用户名/Android/Sdk`
  - CMake: `/usr` 或 `/usr/local`
  
- **Windows**:
  - SDK: `C:\\Users\\用户名\\AppData\\Local\\Android\\Sdk`
  - NDK: `C:\\Users\\用户名\\AppData\\Local\\Android\\Sdk\\ndk\\r18b`
  - CMake: `C:\\Program Files\\CMake`

**注意**: Windows 路径需要使用双反斜杠 `\\` 或正斜杠 `/`。

### 2. 验证 NDK 版本

确保使用的是 NDK r17c 或 r18b:

```bash
# 检查 NDK 目录
ls -la ~/Library/Android/sdk/ndk/
# 或
ls -la ~/Android/Sdk/ndk/
```

你应该看到类似 `r18b` 或 `17.2.4988734` 的目录。

## 构建项目

### 方法 1: 使用 Android Studio (推荐)

1. **打开项目**
   - 启动 Android Studio
   - 选择 **File → Open**
   - 导航到 `drishti/android-studio` 目录
   - 点击 **OK**

2. **等待 Gradle 同步**
   - 第一次打开项目时，Android Studio 会自动同步 Gradle
   - 这可能需要几分钟时间，因为需要下载依赖
   - 如果同步失败，检查 `local.properties` 配置

3. **连接设备或启动模拟器**
   - 通过 USB 连接 Android 设备，并启用 USB 调试
   - 或者在 AVD Manager 中创建并启动模拟器

4. **运行应用**
   - 点击工具栏上的 **Run** 按钮 (绿色三角形)
   - 或按快捷键 **Shift + F10** (Windows/Linux) 或 **Control + R** (macOS)
   - 选择目标设备
   - 应用将自动构建并安装到设备上

### 方法 2: 使用命令行

#### 调试版本 (Debug)

```bash
cd drishti/android-studio
./gradlew assembleDebug
```

#### 发布版本 (Release)

```bash
./gradlew assembleRelease
```

#### 指定架构

```bash
# ARM64 (推荐，适用于大多数现代设备)
./gradlew assembleDebug -Parch=arm64-v8a

# ARMv7 (适用于较老的设备)
./gradlew assembleDebug -Parch=armeabi-v7a

# x86_64 (适用于模拟器)
./gradlew assembleDebug -Parch=x86_64
```

#### 安装到设备

```bash
# 构建并安装 Debug 版本
./gradlew installDebug

# 构建、安装并运行
adb install -r app/build/outputs/apk/debug/app-debug.apk
```

### 方法 3: 使用 Polly (跨平台构建)

对于更高级的构建选项，可以使用 Polly 工具链:

```bash
# 安装 Polly
git clone https://github.com/ruslo/polly
export PATH=`pwd`/polly/bin:$PATH

# 使用指定的工具链构建
polly.py --toolchain android-ndk-r17-api-24-arm64-v8a-clang-libcxx14 \
         --config-all Release \
         --install \
         --verbose \
         --fwd DRISHTI_BUILD_EXAMPLES=ON
```

## 常见问题

### 1. NDK 版本不兼容

**问题**: 错误信息提到 NDK r19 或更高版本不兼容。

**解决方案**:
- 在 `local.properties` 中指定 NDK r17c 或 r18b 的路径
- 如果已安装 r19+，从 SDK Manager 卸载它
- 从 [NDK 旧版本下载页](https://developer.android.com/ndk/downloads/older_releases) 下载 r18b

### 2. CMake 未找到

**问题**: "CMake not found" 错误。

**解决方案**:
```bash
# 验证 CMake 安装
cmake --version

# 在 local.properties 中设置正确的路径
cmake.dir=/path/to/cmake
```

`cmake.dir` 应该指向包含 `bin/cmake` 可执行文件的目录。

### 3. Gradle 同步失败

**问题**: "Failed to sync Gradle project" 错误。

**解决方案**:
1. 检查网络连接 (需要下载依赖)
2. 在 Android Studio 中: **File → Invalidate Caches / Restart**
3. 删除 `.gradle` 目录并重试:
   ```bash
   cd android-studio
   rm -rf .gradle
   ./gradlew clean
   ```

### 4. Hunter 包管理器下载缓慢

**问题**: 首次构建时 Hunter 下载依赖很慢。

**解决方案**:
- Hunter 会将所有依赖缓存到 `~/.hunter` 目录
- 首次构建可能需要 20-60 分钟
- 后续构建会重用缓存，速度会快得多
- 可以使用 `-DHUNTER_STATUS_DEBUG=ON` 查看下载进度

### 5. 构建时内存不足

**问题**: Gradle 构建过程中内存不足。

**解决方案**:

在 `android-studio/gradle.properties` 中增加内存限制:
```properties
org.gradle.jvmargs=-Xmx4096m -XX:MaxPermSize=512m
```

### 6. 设备权限问题

**问题**: 应用启动时摄像头权限被拒绝。

**解决方案**:
- 在设备的设置中手动授予应用摄像头权限
- 或者在应用首次运行时允许权限请求

### 7. CMake 配置错误

**问题**: "Conversion = c, Flags =" 错误。

**解决方案** (临时解决方法):

1. 编辑 `drishti/CMakeLists.txt`
2. 找到 `if(DRISHTI_DEBUG_STOP)` 条件
3. 临时改为 `if(TRUE)`
4. 运行 `./gradlew assembleDebug`
5. 等待几秒后重试
6. 成功后恢复原来的 `if(DRISHTI_DEBUG_STOP)`

## 项目结构

### 主项目结构

```
drishti/
├── android-studio/              # Android Studio 主项目
│   ├── app/                     # 应用模块
│   ├── build.gradle            # 项目级构建配置
│   ├── settings.gradle         # 项目设置
│   └── local.properties        # 本地配置 (需要创建)
│
├── src/examples/facefilter/
│   └── android-studio/         # Face Filter 示例项目
│       ├── app/                # 应用模块
│       │   ├── src/main/
│       │   │   ├── java/       # Java 源代码
│       │   │   ├── res/        # Android 资源
│       │   │   └── AndroidManifest.xml
│       │   ├── build.gradle    # 应用级构建配置
│       │   └── CMakeLists.txt  # C++ 构建配置
│       ├── build.gradle
│       └── local.properties    # 本地配置 (需要创建)
│
├── CMakeLists.txt              # 根 CMake 配置
├── README.rst                  # 主 README (英文)
└── ANDROID_STUDIO_SETUP_CN.md  # 本文档
```

### Face Filter 应用结构

```
app/src/main/java/com/elucideye/facefilter/
├── FaceFilterActivity.java           # 主活动
├── FaceFilterFragment.java           # UI 片段  
├── FaceFilterRenderer.java           # OpenGL 渲染器
├── FaceFilterGLSurfaceView.java      # GL 表面视图
├── FaceFilterCameraManager.java      # 相机管理
├── FaceFilterCameraStateCallback.java    # 相机状态回调
└── FaceFilterCameraSessionCallback.java  # 相机会话回调
```

## 应用功能

Drishti Face Filter 应用提供以下功能:

- **实时人脸检测**: 使用摄像头实时检测人脸
- **眼睛追踪**: 追踪眼睛位置和虹膜
- **面部特征点**: 检测面部关键点
- **OpenGL 渲染**: 使用 OpenGL ES 2.0/3.0 进行实时渲染
- **相机集成**: 使用 Camera2 API 进行高效的相机访问

## 应用要求

- **最低 SDK 版本**: API 24 (Android 7.0)
- **目标 SDK 版本**: API 27 (Android 8.1)
- **所需权限**: CAMERA
- **硬件要求**: 相机、自动对焦

## 技术栈

- **前端**: Java, XML (Android UI)
- **后端**: C++ (Drishti SDK)
- **图形**: OpenGL ES 2.0/3.0
- **构建**: Gradle + CMake
- **包管理**: Hunter
- **相机**: Android Camera2 API

## 开发技巧

### 1. 增量构建

为了加快开发速度，可以只构建特定架构:

```bash
./gradlew assembleDebug -Parch=arm64-v8a
```

### 2. 查看构建日志

```bash
./gradlew assembleDebug --info
./gradlew assembleDebug --debug
```

### 3. 清理构建

```bash
./gradlew clean
```

### 4. 检查依赖

```bash
./gradlew dependencies
```

### 5. 使用 logcat 调试

```bash
# 查看应用日志
adb logcat | grep FaceFilter

# 查看原生日志
adb logcat | grep -i native
```

## 进一步资源

- **主 README**: [README.rst](README.rst) - 详细的项目文档
- **Face Filter README**: [src/examples/facefilter/android-studio/README.md](src/examples/facefilter/android-studio/README.md)
- **Hunter 文档**: https://docs.hunter.sh/
- **Polly 文档**: https://polly.readthedocs.io/
- **Android NDK**: https://developer.android.com/ndk
- **CMake 文档**: https://cmake.org/documentation/

## 贡献

如果在本地开发过程中遇到问题或有改进建议，欢迎提交 Issue 或 Pull Request。

## 许可证

本项目采用 BSD 3-Clause 许可证。详见 LICENSE 文件。

---

**最后更新**: 2024-11-05

**维护者**: Elucideye, Inc.

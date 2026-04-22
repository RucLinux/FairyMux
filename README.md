# FairyMux 音视频工具

基于 `PyQt5 + FFmpeg` 的一站式音视频处理工具，支持批量处理、字幕、录屏、转码、提取、AI 字幕、声音克隆等能力。  
版本：`1.05`  
开发者：海南仙岛  
官网：[https://www.myzhenai.com.cn/](https://www.myzhenai.com.cn/)

---

## 下载（主程序 / 插件 / 模型）

可通过以下网盘下载 FairyMux 主程序，以及插件和模型资源（RTVC / SoVITS / Whisper）：

- 百度网盘：<https://pan.baidu.com/s/1cu9RomarbHZmaxm5fYaKFg?pwd=79uu>（提取码：`79uu`）
- 夸克网盘：<https://pan.quark.cn/s/68226354d0df?pwd=WqYX>（提取码：`WqYX`）
- 天翼网盘：<https://cloud.189.cn/t/zUbmE3EVJjUj>（访问码：`zw01`）

> 提示：如暂不使用高级功能，可先不下载 RTVC / SoVITS / Whisper 大模型目录，仅使用核心音视频功能。

---

## 功能概览

- 工具设置：统一管理 FFmpeg / Whisper / Tesseract 路径，自动检测环境
- 屏幕录制：全屏/区域/窗口录制，支持音频方案
- 视频水印：文字/图片水印，位置、透明度、字体可调
- 视频字幕：硬字幕/软字幕处理，支持批量
- 视频合并：多文件按顺序拼接
- 视频转码：编码、格式、码率、分辨率转换
- 提取字幕：软字幕轨提取 + 硬字幕 OCR 提取
- 视频截图：按规则抓帧、批量截图
- 视频分割：按时长或时间段切割
- 图片转视频：图片序列合成视频
- 视频添加音乐：混音/替换背景音，支持批量
- 提取视频/音频：分离音视频轨道
- 媒体元数据修改：标题、作者、版权等信息编辑
- Whisper 生成字幕：AI 语音识别，多语言模型
- 声音克隆：RTVC / SoVITS 相关流程

---

## 平台支持

### Windows

- 支持版本：Windows 10 / Windows 11（64位）
- 推荐环境：8GB+ 内存、i5/R5 及以上 CPU
- 使用建议：首次启动先在“工具设置”页检查 FFmpeg / Whisper / Tesseract 路径
- AI 功能建议：如使用 RTVC / SoVITS，建议使用 NVIDIA GPU 提升推理速度

### Linux

- 支持发行版：Debian / Ubuntu / Deepin（64位）
- 推荐环境：8GB+ 内存、i5/R5 及以上 CPU
- 依赖建议：先安装 FFmpeg（例如 `sudo apt install ffmpeg`）
- 桌面环境建议：录屏在 X11 下通常比 Wayland 兼容性更好

---

## 使用说明

1. 从上方任一网盘下载 FairyMux 主程序压缩包。
2. 解压后运行程序（Windows 运行 `.exe`，Linux 运行对应启动文件）。
3. 打开“工具设置”，检查 FFmpeg / Whisper / Tesseract 路径。
4. 如需声音克隆或 AI 字幕，再下载并放置对应插件与模型目录。

---

## Linux 无法运行排查

如果用户反馈 Linux 下无法启动，请在 **Linux 终端** 执行以下命令（把路径改成实际安装目录）并回传完整输出：

```bash
uname -m
cd /实际安装目录
file ./FairyMux
chmod +x run.sh FairyMux
./run.sh
# 或
./FairyMux
ls -R
```

说明：

- `uname -m` 用于确认 CPU 架构（如 `x86_64` / `aarch64`）
- `file ./FairyMux` 用于确认可执行文件架构与格式
- `chmod +x` 用于补齐执行权限
- `ls -R` 用于核对安装目录文件是否完整
- 请务必在 Linux 机器上执行，不要在 Windows PowerShell 中执行

---

## 推荐目录结构

```text
FairyMux/
├── ffmpeg.exe             # FFmpeg 可执行文件（可选）
├── whisper.exe            # Whisper 可执行文件（可选）
├── tesseract.exe          # Tesseract 可执行文件（可选）
├── fonts/                 # 字体文件目录
├── Plugin/                # 插件目录
│   ├── RTVC/
│   │   └── Real-Time-Voice-Cloning/
│   │       ├── pretrained_models/
│   │       │   ├── encoder/encoder.pt
│   │       │   ├── synthesizer/synthesizer.pt
│   │       │   └── vocoder/vocoder.pt
│   │       └── saved_models/default/   # 旧结构兼容
│   ├── SoVITS/
│   │   └── so-vits-svc/
│   │       ├── configs/config.json
│   │       ├── logs/44k/
│   │       ├── trained/
│   │       ├── pretrain/
│   │       ├── inference_main.py
│   │       ├── raw/
│   │       └── results/
│   └── whisper/
│       ├── whisper.exe
│       └── models/
├── img/                   # 图片资源目录
└── version.json           # 版本信息文件
```

---

## 常见问题（FAQ）

### 1) 提示找不到 FFmpeg

请确认 FFmpeg 已正确安装并加入系统环境变量，或将 `ffmpeg.exe` 放到程序同目录。

### 2) SoVITS 说话人下拉框为空

检查 `config.json` 是否包含说话人信息，例如：

```json
"spk": {"说话人1": 0, "说话人2": 1}
```

### 3) Whisper 模型检测失败

请确认模型文件位于 `Plugin/whisper/models` 目录（或你在设置中指定的目录）。

### 4) RTVC 模型检测失败

请确认以下文件存在且完整：

- `encoder.pt`
- `synthesizer.pt`
- `vocoder.pt`

### 5) SoVITS 报错 “The name you entered is not in the speaker list!”

请从说话人下拉框选择与 `config.json` 中完全一致的名称。

### 6) 声音克隆处理速度慢

属正常现象。AI 推理计算量大，CPU 显著慢于 GPU。

---

## 技术支持

- 官方网站：[https://www.myzhenai.com.cn/](https://www.myzhenai.com.cn/)
- 技术博客：[https://jiayu.mybabya.com/](https://jiayu.mybabya.com/)

© 2025-2026 版权所有：海南仙岛 | JiaYu Blog

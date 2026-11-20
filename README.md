# PureCam 13 — Native Android Camera App for OnePlus 13

**PureCam 13** is a native Kotlin + Camera2 API + Jetpack Compose Android camera application engineered specifically for the **OnePlus 13** (Snapdragon 8 Elite, OxygenOS 15 / Android 15). It combines:

- **Google Camera (GCam) Design Layout**: AMOLED black viewfinder, minimalist top pill bar, floating optical zoom pills (`0.6x`, `1x`, `2x`, `3x`, `6x`), dual on-screen EV/WB sliders, horizontal mode switcher, and classic circular shutter deck with pull-up Quick Settings.
- **Samsung Camera Features**: Draggable Floating Shutter button, Pro Video mode (up to 4K60 / 8K30 HEVC with live L/R stereo RMS audio meter and mic selector), Dual Recording (concurrent rear + front PiP/Split-screen via `concurrentCameraIds`), 12MP/50MP quick toggle, configurable hardware Volume Key shutter/zoom, gridlines, and self-timer.
- **Sony Xperia (Photography Pro) Optimization & Strict Zero-AI Pipeline**:
  - **Zero AI dependencies**: No TensorFlow Lite, ML Kit, ONNX, NNAPI, or OEM AI CameraX Extensions.
  - **Direct Camera2 HAL control**: Explicitly disables `CONTROL_SCENE_MODE`, `CONTROL_EFFECT_MODE`, aggressive AI noise smearing (`NOISE_REDUCTION_MODE_OFF` / `MINIMAL`), and oversharpening halos (`EDGE_MODE_OFF`).
  - **True 10/12-bit RAW DNG (`RAW_SENSOR`)** via `DngCreator` alongside deterministic JPEG and `RAW+JPG` capture.
  - **Manual Pro Controls**: `P / S / M / MR1 / MR2 / MR3` exposure dial with persistent Memory Recall presets, ISO, Shutter Speed (`1/8000s` to `30s`), Manual Focus diopter slider, Planckian-locus Kelvin White Balance (`2300K`–`9000K`), EV compensation, `AE-L` / `AF-L` locks, continuous high-speed burst (long-press shutter), real-time deterministic RGB/Luma Histogram, Sobel Focus Peaking, Zebra Stripes (95% highlight clipping), and 3-axis Hardware Spirit Level.

## OnePlus 13 Sensor Mapping

`OnePlus13CameraCatalog.kt` dynamically enumerates standalone and physical multi-camera IDs by focal length and aperture to map the OnePlus 13's hardware ([PhoneArena](https://www.phonearena.com/news/oneplus-13-camera_id164056), [PetaPixel](https://petapixel.com/2025/01/17/oneplus-13-review-this-smartphone-is-the-total-package/), [Digital Camera World](https://www.digitalcameraworld.com/tech/android-phones/oneplus-13-review)):

| Zoom Pill | Sensor | Optics & Stabilization |
| :--- | :--- | :--- |
| **0.6x** | 50MP Samsung ISOCELL JN5 (1/2.75") | 15mm equiv., f/2.0, 120° FOV, PDAF |
| **1x / 2x** | 50MP Sony LYT-808 (1/1.4") | 23mm equiv., f/1.6, OIS, PDAF (2x pure sensor crop) |
| **3x / 6x** | 50MP Sony LYT-600 Triprism (1/1.95") | 73mm equiv., f/2.6, OIS, PDAF (6x pure sensor crop) |
| **Front** | 32MP Sony IMX615 (1/2.74") | 25mm equiv., f/2.4, fixed focus |

## How to Build & Install on Your OnePlus 13

### Option 1: Android Studio (Recommended)
1. Unzip `OnePlus13-PureCam-Android.zip`.
2. Open the `OnePlus13-PureCam` folder in **Android Studio (Ladybug / Meerkat or newer)** with **JDK 17** and **Android SDK 35**.
3. Let Gradle sync, connect your OnePlus 13 via USB (with USB Debugging enabled), and click **Run ▶** — or choose **Build → Build Bundle(s) / APK(s) → Build APK(s)**.

### Option 2: Cloud APK Build via GitHub Actions (No Local Android Studio Needed)
1. Upload the unzipped `OnePlus13-PureCam` folder to a new GitHub repository.
2. Open the **Actions** tab and run **Build PureCam 13 APK** (`.github/workflows/build-apk.yml`).
3. Download the compiled `PureCam13-debug-apk` artifact and sideload it onto your OnePlus 13.

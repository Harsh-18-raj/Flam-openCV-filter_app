# 🎥 **OpenCV Filter App**

### _Real-Time Camera Filters using Kotlin + OpenCV + Native C++ (JNI)_

> A high-performance Android application that applies **real-time camera filters** using **Camera2 API** and **OpenCV (C++)**.  
> Delivers instant visual effects like *Cartoon*, *Edge Detection*, *Blur*, and *Grayscale* — all rendered natively for maximum FPS and smooth performance.  
> Designed with a modern Material UI, fluid animations, and custom feedback to ensure a fast and elegant user experience.

---

## 🌍 **Overview**

The **OpenCV Filter App** bridges **Kotlin** and **C++ (OpenCV)** using the **JNI (Java Native Interface)** for efficient, pixel-level image processing directly in the native layer.

**Workflow:**
1. Captures each frame via **Camera2 TextureView**  
2. Sends it to the **C++ layer (via JNI)**  
3. Applies the selected filter in **real-time**  
4. Displays the processed output instantly  

### 🎯 **User Features**
- Select filters via dropdown menu  
- Adjust filter intensity with a slider  
- Capture and save processed frames  
- Animated thumbnail previews  
- In-app gallery access for saved photos  

---

## 🧩 **Core Features**

| Category | Description |
|-----------|--------------|
| ⚙️ **Real-Time Processing** | Filters applied directly on camera frames using native OpenCV functions. |
| 🎨 **Filter Modes** | *None*, *Cartoon*, *Edge Detection*, *Blur*, *Grayscale* |
| ⚡ **Native Performance** | Pixel operations handled in C++ for low-latency rendering. |
| 📷 **Camera2 Integration** | Modern API ensures stable and high-FPS video stream. |
| 🧭 **Dynamic UI** | Dropdown selector, live slider control, and fluid animations. |
| 💾 **Quick Save** | Photos auto-saved to `/Pictures/OpenCVFilterApp`. |
| 💬 **Interactive Feedback** | Custom animated toasts for save success or errors. |
| 🎚️ **Adjustable Intensity** | Fine-tune edge or blur effects in real time. |
| 🖼️ **Animated Thumbnails** | Smooth transitions when capturing new images. |
| 📂 **Built-in Gallery** | View all captured photos without leaving the app. |
| 💜 **Material Design** | Elegant purple-accent theme with modern typography. |

---

## 🧠 **Tech Stack**

| Layer | Tools / Frameworks |
|--------|--------------------|
| **Languages** | Kotlin (Android), C++ (Native) |
| **Frameworks** | Camera2 API, OpenCV 4.x |
| **Build System** | Gradle + CMake + Android NDK |
| **UI/UX** | Material Components + ConstraintLayout |
| **Animations** | Android Animator APIs |
| **Storage** | MediaStore + Scoped Storage |

---

## 🧮 **Implemented Filters**

Filters are processed inside the native C++ layer (`native-lib.cpp`) and invoked from Kotlin via JNI.

| ID | Filter | Description |
|----|---------|-------------|
| 0 | **None** | Displays the original camera frame. |
| 1 | **Cartoon** | Combines edge detection + color quantization for a cartoon-like look. |
| 2 | **Edge Detection** | Uses the Canny detector, adjustable via intensity. |
| 3 | **Blur** | Applies Gaussian blur proportional to slider intensity. |
| 4 | **Grayscale** | Converts frame into monochrome output. |

---

### 🧩 **Example — Cartoon Filter (C++ Implementation)**

```cpp
case 1: { // Cartoon Filter
    Mat bgr, gray, edges, color;
    cvtColor(src, bgr, COLOR_RGBA2BGR);
    cvtColor(bgr, gray, COLOR_BGR2GRAY);
    medianBlur(gray, gray, 5);
    Laplacian(gray, edges, CV_8U, 5);
    threshold(edges, edges, 100, 255, THRESH_BINARY_INV);
    Mat small; 
    pyrDown(bgr, small); 
    pyrDown(small, small);
    pyrUp(small, small); 
    pyrUp(small, small);
    cvtColor(edges, edges, COLOR_GRAY2BGR);
    bitwise_and(small, edges, color);
    cvtColor(color, dst, COLOR_BGR2RGBA);
}
```

---

## 🧱 **System Architecture**

```
📱 Kotlin (MainActivity)
│
│   ├── Captures camera frames via Camera2 API
│   ├── Sends frame + filter ID + intensity → JNI
│   ├── Displays processed output in ImageView
│   ├── Handles capture, animations, and toast feedback
│   └── Updates animated thumbnails
│
└── 🧠 Native Layer (C++ - native-lib.cpp)
    ├── Receives Bitmap data
    ├── Converts ARGB ↔ OpenCV Mat
    ├── Runs OpenCV filter logic
    ├── Returns processed frame
    └── Optimized for speed and memory efficiency
```

---

## 🖥️ **User Interface Flow**

### 🎛️ **Filter Dropdown**
- Default: “🎨 Select Filter”
- Options: None | Cartoon | Edge | Blur | Grayscale  
- Intensity slider auto-hides when not required.

### 🎚️ **Intensity Slider**
- Adjusts blur radius or edge thresholds.
- Displays value as `Filter Intensity: 0–100%`.

### 📸 **Capture Button**
- Captures the current processed frame.  
- Adds flash + vibration effect.  
- Saves the image to `/Pictures/OpenCVFilterApp`.

### 🖼️ **Animated Thumbnail**
- Old image slides up + fades.  
- New capture fades in from bottom.  
- Tap thumbnail → Opens system gallery.

### 💬 **Custom Toast**
- Message: “📸 Image Saved Successfully!”  
- Styled with purple background, shadows, and fade-in animation.

---

## ⚙️ **Build & Installation Guide**

### 🔧 **Requirements**
- Android Studio **Flamingo (or newer)**  
- Installed **NDK** + **CMake** via SDK Manager  
- Downloaded **OpenCV SDK for Android**

### 🪜 **Setup Steps**

```bash
# Clone the repository
git clone https://github.com/Harsh-18-raj/Flam-openCV-filter_app.git
cd Flam-openCV-filter_app

# Open in Android Studio
# Allow Gradle to sync and build automatically

# Connect Android device (with USB Debugging enabled)
# Hit ▶ Run to launch the app
```

---

## 👨‍💻 **Developer**

**Harsh Raj**  
🎓 IIIT Dharwad, India  

> _“Where creativity meets computer vision — turning every frame into art.”_

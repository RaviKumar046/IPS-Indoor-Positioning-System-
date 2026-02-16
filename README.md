# Indoor Positioning System & Visualization Projects

A collection of interactive web applications and simulations for indoor positioning, WiFi tracking, and physics visualizations.

## 🎯 Projects Overview

### 📍 Indoor Positioning System (IPS)

WiFi-based indoor positioning system using ESP32 devices and fingerprinting algorithms.

#### Features
- **Real-time location tracking** with probability-based positioning
- **ESP32 Tag Interface** - Monitor and track ESP32 device positions
- **WiFi Survey Tool** - Collect training data for positioning algorithms
- **Live visualization** of location probabilities and confidence scores
- **RESTful API integration** for real-time data updates

#### Components

**ESP32 Tag Tracker** ([ESP32.html](ESP32.html))
- Modern, responsive interface for tracking ESP32 devices
- Displays location probabilities with visual confidence indicators
- Real-time updates with API integration
- Top-3 location display with probability bars

**WiFi Survey Tool** ([wifisurvey.py](wifisurvey.py))
```bash
# Install dependencies
pip install pywifi

# Run the survey tool
python wifisurvey.py
```
- Collects WiFi RSSI data for training positioning algorithms
- Burst scanning mode for accurate fingerprinting
- CSV export for machine learning datasets

**Live Position Tracker** ([gps.html](gps.html))
- Web-based interface for real-time indoor positioning
- Visualizes WiFi-based location tracking
- Designed for continuous monitoring applications

---

### 🌌 Black Hole Simulation

Real-time gravitational lensing and orbital mechanics visualization using OpenGL.

#### Features
- ✨ Real-time raytracing with gravitational lensing
- 🌌 Accretion disk visualization around Sagittarius A*
- 🪐 N-body orbital mechanics simulation
- 📐 Spacetime grid warping visualization
- 🎮 Interactive camera controls

#### Quick Start

**Dependencies** (via vcpkg)
```powershell
vcpkg install glew:x64-windows glfw3:x64-windows glm:x64-windows
```

**Compile & Run**
```powershell
# Windows (MSVC)
cl /EHsc blackhole.cpp /I"<vcpkg>/installed/x64-windows/include" /link /LIBPATH:"<vcpkg>/installed/x64-windows/lib" glew32.lib glfw3dll.lib opengl32.lib

# Linux (GCC)
g++ -std=c++17 blackhole.cpp -o blackhole -lGL -lGLEW -lglfw -lm
```

**Controls**
- **Left Mouse Drag** - Orbit camera
- **Mouse Scroll** - Zoom
- **G Key** - Toggle gravitational physics
- **ESC** - Exit

See [README_BLACKHOLE.md](README_BLACKHOLE.md) for detailed documentation.

---

### 📡 WiFi Tracker Applications

Two modern React-based WiFi tracking interfaces built with Vite.

#### My-Wifi-Tracker
```bash
cd My-Wifi-Tracker
npm install
npm run dev
```

#### Wifi-Tracker
```bash
cd Wifi-Tracker
npm install
npm run dev
```

Both projects provide modern, responsive interfaces for WiFi network monitoring and indoor positioning visualization.

---

## 🚀 Getting Started

### Prerequisites

**For Web Applications:**
- Modern web browser (Chrome, Firefox, Edge, Safari)
- Node.js 16+ (for React projects)
- Python 3.8+ (for WiFi survey tool)

**For Black Hole Simulation:**
- OpenGL 4.3+ compatible GPU
- GLEW, GLFW3, GLM libraries
- C++17 compatible compiler (MSVC, GCC, or Clang)

### Installation

1. **Clone the repository**
   ```bash
   git clone <your-repo-url>
   cd IPS
   ```

2. **For WiFi Survey (Python)**
   ```bash
   pip install pywifi
   python wifisurvey.py
   ```

3. **For React Projects**
   ```bash
   cd My-Wifi-Tracker
   npm install
   npm run dev
   ```

4. **For Black Hole Simulation**
   - Install dependencies via vcpkg
   - Compile using provided commands (see Black Hole section)

---

## 📊 Project Structure

```
IPS/
├── ESP32.html              # ESP32 tag tracking interface
├── ESP32_Tag.html          # Alternative ESP32 interface
├── gps.html                # WiFi indoor positioning tracker
├── wifisurvey.py           # WiFi fingerprinting data collection
├── script.js               # Frontend logic for IPS
├── style.css               # Shared styles
├── blackhole.cpp           # Black hole simulation (C++/OpenGL)
├── geodesic.comp           # Compute shader for raytracing
├── grid.vert/grid.frag     # Grid visualization shaders
├── map.json/newmap.json    # Location mapping data
├── My-Wifi-Tracker/        # React WiFi tracker (Vite)
├── Wifi-Tracker/           # Alternative WiFi tracker (Vite)
└── vcpkg/                  # C++ package manager
```

---

## 🛠️ Technologies Used

### Web Stack
- **HTML5/CSS3** - Modern, responsive UI
- **JavaScript (ES6+)** - Interactive functionality
- **React 18** - Component-based architecture
- **Vite** - Fast development and build tooling

### Backend & Data Collection
- **Python 3** - WiFi survey and data processing
- **PyWiFi** - Cross-platform WiFi scanning
- **CSV** - Training data storage

### Graphics & Simulation
- **C++17** - High-performance computation
- **OpenGL 4.3+** - Real-time rendering
- **GLSL** - Custom shaders for raytracing
- **GLEW/GLFW3** - Window and context management

---

## 📡 WiFi Indoor Positioning System

### How It Works

1. **Fingerprinting Phase**
   - Use `wifisurvey.py` to collect WiFi RSSI values at known locations
   - Data is saved to CSV for training machine learning models

2. **Positioning Phase**
   - ESP32 devices scan WiFi networks and send RSSI data to server
   - Server compares against fingerprint database
   - Returns location probabilities using k-NN or similar algorithms

3. **Visualization**
   - Web interfaces display real-time position with confidence scores
   - Top-3 locations shown with probability bars

### API Integration

The system expects a REST API endpoint returning JSON:
```json
{
  "locations": [
    {"name": "Room A", "probability": 0.85},
    {"name": "Room B", "probability": 0.10},
    {"name": "Room C", "probability": 0.05}
  ],
  "timestamp": "2026-02-16T10:30:00Z"
}
```

---

## 🎮 Interactive Demos

- **[ESP32 Tracker](ESP32.html)** - Monitor indoor position in real-time
- **[GPS/WiFi Tracker](gps.html)** - Live WiFi-based positioning
- **[Black Hole Simulation](blackhole.cpp)** - Physics visualization
- Various experimental demos: `sq.html`, `sqchat.html`, `fu.html`

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit pull requests or open issues for bugs and feature requests.

### Development Workflow

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

## 🙏 Acknowledgments

- **WiFi Positioning** - Based on fingerprinting algorithms and RSSI measurements
- **Black Hole Physics** - Schwarzschild metric for gravitational lensing
- **ESP32** - Espressif Systems for affordable IoT hardware
- **vcpkg** - Microsoft for C++ package management

---

## 📧 Contact

For questions or collaboration opportunities, please open an issue on GitHub.

---

## 🔗 Quick Links

- [Black Hole Documentation](README_BLACKHOLE.md)
- [vcpkg Package Manager](https://github.com/microsoft/vcpkg)
- [ESP32 Development](https://www.espressif.com/en/products/socs/esp32)

---

**⭐ If you find this project useful, please consider giving it a star!**

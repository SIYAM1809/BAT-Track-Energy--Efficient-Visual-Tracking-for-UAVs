# BAT-Track: Battery-Aware Adaptive Visual Tracking for UAVs

Official implementation of "BAT-Track: Battery-Aware Adaptive Visual Tracking for Resource-Constrained UAVs".

## Overview

BAT-Track is a novel battery-aware adaptive tracking system that dynamically switches between high-accuracy and efficient trackers based on real-time battery levels, achieving optimal accuracy-energy trade-offs for UAV applications.

## Key Results

- **64.2% IoU** on UAV123 dataset (123 sequences)
- **60.5% energy savings** compared to OSTrack baseline
- **Real-time performance** at 39.3 FPS
- **6.1% accuracy improvement** over pure efficient tracker

## 🎬 Demo Videos



### Adaptive Tracker Switching in Action

BAT-Track dynamically switches between **OSTrack** (🔋 &gt;70%, 🟡 **Yellow BBox**) and **SiamAPN++** (🔋 ≤70%, 🔴 **Red BBox**) based on real-time battery levels.

| Building | Car |
|:---:|:---:|
| [![Building](https://img.youtube.com/vi/Tf39Zdd8d5Y/0.jpg)](https://youtu.be/Tf39Zdd8d5Y) | [![Car](https://img.youtube.com/vi/fJssBVbzK2k/0.jpg)](https://youtu.be/fJssBVbzK2k) |
| **🏢 Building Tracking** | **🚗 Vehicle Tracking** |
| Structure monitoring | High-speed ground tracking |

| Person | Truck |
|:---:|:---:|
| [![Person](https://img.youtube.com/vi/lVudh3ygCnA/0.jpg)](https://youtu.be/lVudh3ygCnA) | [![Truck](https://img.youtube.com/vi/u-kuVsdbiMo/0.jpg)](https://youtu.be/u-kuVsdbiMo) |
| **🚶 Person Tracking** | **🚛 Truck Tracking** |
| Pedestrian surveillance | Heavy vehicle logistics |


### 🎨 Color Coding Legend
| Color | Tracker | Battery Condition | Characteristics |
|:-----:|:-------:|:-----------------:|:---------------|
| 🟡 **Yellow** | OSTrack | &gt; 70% | High accuracy, higher energy |
| 🔴 **Red** | SiamAPN++ | ≤ 70% | Energy-efficient, faster FPS |

## Requirements
```bash
Python 3.8+
PyTorch 1.12+
OpenCV 4.5+
numpy, pandas, matplotlib
```

## Installation
```bash
# Clone repositories
git clone https://github.com/botaoye/OSTrack
git clone https://github.com/vision4robotics/SiamAPN

# Install dependencies
pip install -r requirements.txt
```

## Usage

### Quick Start
```python
from battrack import BATTrack_v2_Energy

# Initialize tracker
tracker = BATTrack_v2_Energy(initial_battery_percent=80.0)

# Track sequence
tracker.initialize(first_frame, init_bbox)
for frame in frames:
    bbox, info = tracker.track(frame)
```

### Full Evaluation
```bash
python evaluate_battrack.py --dataset UAV123 --output results.csv
```

## Results

| Method | IoU | Energy (Wh) | Energy Saved | FPS |
|--------|-----|-------------|--------------|-----|
| OSTrack | 73.1% | 46.86 | 0% | 18.5 |
| SiamAPN++ | 58.1% | 15.62 | 66.7% | 64.9 |
| **BAT-Track** | **64.2%** | **18.51** | **60.5%** | **39.3** |


## Acknowledgments

- OSTrack: [GitHub](https://github.com/botaoye/OSTrack)
- SiamAPN: [GitHub](https://github.com/vision4robotics/SiamAPN)
- UAV123 Dataset: [Website](https://cemse.kaust.edu.sa/ivul/uav123)

## License

MIT License
```

---

# **📦 FINAL FILE ORGANIZATION**

Create this structure before zipping:
```text
BAT-Track-Project/
│
├── README.md                              # ⭐ Professional documentation
├── requirements.txt                       # Python dependencies
├── LICENSE                                # MIT/Apache license
│
├── code/
│   ├── battrack_v2_energy.py            # Main BAT-Track class
│   ├── evaluate_ostrack.py              # OSTrack evaluation
│   ├── evaluate_siamapn.py              # SiamAPN++ evaluation
│   ├── evaluate_battrack.py             # BAT-Track evaluation
│   └── generate_figures.py              # All figure generation code
│
├── results/
│   ├── ostrack_baseline_full_results.csv
│   ├── siamapn_baseline_full_results.csv
│   └── battrack_v2_full_results.csv
│
├── figures/
│   ├── figure1_overall_comparison.png    # All 17 figures
│   ├── figure2_pareto_frontier.png
│   ├── ...
│   └── figure17_qualitative_results.png
│
├── videos/
│   ├── battrack_demo_video.mp4
│   └── battrack_comparison_video.mp4
│
├── paper/
│   ├── latex_tables.txt                  # Copy-paste LaTeX tables
│   ├── abstract.txt                      # Ready-to-use abstract
│   └── conclusion.txt                    # Ready-to-use conclusion
│
└── supplementary/
    └── analysis_notebooks.ipynb          # Additional analysis

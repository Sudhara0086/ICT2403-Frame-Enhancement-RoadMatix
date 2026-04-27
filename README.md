# ICT2403 – Graphics and Image Processing
## Road Surface Damage Detection System
**Rajarata University of Sri Lanka | Department of Computing**

---

## Project Overview
This project develops a video-based image processing system to detect and segment road surface damage from recorded road video footage. The system processes video frames through enhancement and segmentation stages to identify four types of road damage: Potholes, Edge Cracks, Alligator Cracks, and Raveling.

---

## Team Members
| Member | Index No | Reg No | Responsibility |
|--------|----------|--------|----------------|
| Member 1 | 6010 | ICT/2023/017 | Pothole Segmentation |
| Member 2 | 6012 | ICT/2023/019 | Edge Crack Segmentation |
| Member 3 | 6009 | ICT/2023/016 | Alligator Crack Segmentation |
| Member 4 | 6011 | ICT/2023/018 | Raveling Segmentation + Integration |

---

## Repository Structure

```
ICT2403-RoadDamageDetection/
│
├── road_video.mp4                    # Original recorded road video
│
├── Frames/                           # Extracted original frames from video
│
├── Final_Enhanced/                   # Enhanced frames (noise removed, contrast improved)
├── Final_Segmented/                  # Binary segmentation masks (all 4 damage types)
├── Final_Marked/                     # Frames with all damage types marked in colour
├── Final_Comparisons/                # 4-panel pipeline comparison images (first 5 frames)
│
├── Member1_Segmentation/             # Pothole outputs + pothole_metrics.txt
├── Member2_Segmentation/             # Edge crack outputs + edgecrack_metrics.txt
├── Member3_Segmentation/             # Alligator crack outputs + alligator_metrics.txt
├── Member4_Segmentation/             # Raveling outputs + raveling_metrics.txt
│
├── GroundTruth_Potholes/             # 15 manually drawn pothole ground truth masks
├── GroundTruth_EdgeCracks/           # 15 manually drawn edge crack ground truth masks
├── GroundTruth_AlligatorCracks/      # 15 manually drawn alligator crack ground truth masks
├── GroundTruth_Raveling/             # 15 manually drawn raveling ground truth masks
│
├── main_pipeline_seg.ipynb           # MAIN FILE - runs complete pipeline (enhancement + segmentation)
├── Main_Pipeline_Enhan.ipynb         # Enhancement pipeline only
│
├── member1_segmentation.ipynb        # Pothole segmentation code
├── member2_segmentation.ipynb        # Edge crack segmentation code
├── member3_segmentation.ipynb        # Alligator crack segmentation code
├── member4_segmentation.ipynb        # Raveling segmentation code
│
├── member1_enhancement.ipynb         # Noise removal (Submission 03)
├── member2_enhancement.ipynb         # Contrast enhancement - CLAHE (Submission 03)
├── member3_enhancement.ipynb         # Sharpening (Submission 03)
│
└── README.md                         # This file
```

---

## How to Run the Full Pipeline

### Requirements
- Python 3.x
- Anaconda Navigator + Jupyter Notebook
- Libraries: OpenCV, NumPy, Matplotlib

### Steps
1. Make sure all extracted frames are in the `Frames/` folder
2. Open **Anaconda Navigator** and launch **Jupyter Notebook**
3. Navigate to the project folder
4. Open **`main_pipeline_seg.ipynb`**
5. Run all cells
6. All outputs are saved automatically:
   - Enhanced frames → `Final_Enhanced/`
   - Segmentation masks → `Final_Segmented/`
   - Marked outputs → `Final_Marked/`
   - Comparison images → `Final_Comparisons/`

---

## Submission 03 – Frame Enhancement

### Enhancement Pipeline
Each frame goes through three enhancement stages:

| Stage                 | Method                                     | Code File                 |
|-----------------------|--------------------------------------------|---------------------------|
| Noise Removal         | Median Filter (5×5 kernel)                 | member1_enhancement.ipynb |
| Contrast Enhancement  | CLAHE (clipLimit=2.0, tileGridSize=8×8)    | member2_enhancement.ipynb |
| Sharpening            | Unsharp Masking (Laplacian variance < 400) | member3_enhancement.ipynb |

### Run Enhancement Only
Open `Main_Pipeline_Enhan.ipynb` and run all cells.

---

## Submission 04 – Segmentation and Evaluation

### Damage Types Detected
| Colour in Output | Damage Type     | Member   | Code File                  |
|------------------|-----------------|----------|----------------------------|
| Red              | Pothole         | Member 1 | member1_segmentation.ipynb |
| Green            | Edge Crack      | Member 2 | member2_segmentation.ipynb |
| Orange           | Alligator Crack | Member 3 | member3_segmentation.ipynb |
| Purple           | Raveling        | Member 4 | member4_segmentation.ipynb |

### Segmentation Methods Summary
| Damage Type     | Method                                                                |
|-----------------|-----------------------------------------------------------------------|
| Pothole         | ROI masking + Bright/Dark binary threshold + Per-frame kernel sizing  |
| Edge Crack      | Left-zone ROI + HSV filtering + Adaptive Gaussian threshold           |
| Alligator Crack | Polygon ROI (3 groups) + Fixed threshold + Large 31x31 closing kernel |
| Raveling        | Central ROI + Top-hat operation + Fixed threshold = 30                |

### Evaluation Results Summary
| Damage Type     | Accuracy | Precision | Recall | F1     | IoU    |
|-----------------|----------|-----------|--------|--------| -------|
| Pothole         | 0.8789   | 0.4938    | 0.8562 | 0.5242 | 0.3662 |
| Edge Crack      | 0.9154   | 0.5911    | 0.3084 | 0.4016 | 0.2534 |
| Alligator Crack | 0.8637   | 0.7008    | 0.4796 | 0.5673 | 0.4203 |
| Raveling        | 0.4358   | 0.8428    | 0.2183 | 0.3387 | 0.2076 |

---

## Ground Truth Masks
Each member manually prepared 15 ground truth masks by painting the damage area white and background black. Masks are stored in the GroundTruth folders and used for quantitative evaluation using Accuracy, Precision, Recall, F1, IoU, and Dice metrics.

---

## Notes
- All frames were extracted from a single road video (road_video.mp4)
- Frame resolution: 848 x 478 pixels, JPEG format
- Frames were manually sorted into damage type folders before segmentation
- Enhanced frames from Submission 03 (Final_Enhanced/) were used directly as input for Submission 04 segmentation

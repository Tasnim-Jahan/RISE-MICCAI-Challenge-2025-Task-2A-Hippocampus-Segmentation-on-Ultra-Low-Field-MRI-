# 🧠 RISE MICCAI Challenge 2025 — Task 2A  
### Hippocampus Segmentation on Ultra-Low-Field MRI

---

## 📄 Overview
This repository contains the training and evaluation pipeline developed for the **RISE MICCAI Challenge 2025 (Task 2A)**, focusing on **bilateral hippocampus segmentation** from ultra-low-field MRI volumes.  
The work implements a **MONAI-based 3D segmentation framework**, emphasizing robust preprocessing, efficient class balancing, and anatomically consistent augmentation strategies.  

---

## Dataset

This code was developed for the **LISA 2025 Challenge**
(*Low-Field Pediatric Brain Magnetic Resonance Image Segmentation and Quality Assurance 2025*).

Dataset source:
> LISA 2025 Challenge Organizers.  
> *LISA 2025: Low-Field Pediatric Brain MRI Segmentation and Quality Assurance Challenge.*  
> Available at: [https://lisa2025.grand-challenge.org](https://lisa2025.grand-challenge.org)

Data are used under the LISA 2025 User License Agreement and cannot be redistributed.

---

## 🧬 Key Features
- **Dataset:** RISE-LISA Task 2A (Ultra-Low-Field MRI of hippocampus)  
- **Framework:** [MONAI](https://monai.io/) with PyTorch backend  
- **Segmentation Type:** 3D binary segmentation (Left + Right hippocampi)  
- **Patch Size:** 64³ (configurable)  
- **Cropping Strategy:** Class-balanced `RandCropByLabelClassesd`  
- **Augmentation:**
  - Random flip (only on **AP/SI axes**, never on LR)  
  - Single pad + crop transform for consistent input shape  
  - Intensity normalization, affine transforms  
- **Model Backbone:** Variants of `UNet` and `Attention UNet`  
- **Evaluation Metrics:** Dice Score, HD, HD95, ASSD, RVE  
- **Inference:** Sliding-window strategy for volumetric predictions  
- **Sanity Checks:** Per-batch voxel-count printouts for L/R class balance  

---

## ⚙️ Pipeline Outline
1. **Data loading** with `LoadImaged` and `LoadLabeld`  
2. **Preprocessing:** orientation, spacing normalization, intensity scaling  
3. **Augmentation:** controlled random transformations (no LR flips)  
4. **Patch sampling:** balanced crops for both hippocampi  
5. **Model training:** 3D UNet variants (CBAM/ECA-enhanced in later experiments)  
6. **Inference:** sliding-window prediction and post-processing  
7. **Evaluation:** Dice Score & HD95 metrics, batch-wise balance logs  

---

## 📊 Official Test-Phase Results (LISA 2025)
| Metric | Average ± SD | Description |
|:--|:--|:--|
| **Mean Error** | 2.204 | Overall volumetric error |
| **DSC (Dice Score)** | **0.56 ± 0.18** | Segmentation overlap |
| **HD (Hausdorff Distance)** | 5.79 ± 1.73 mm | Boundary deviation |
| **HD95 (95th Percentile HD)** | 3.50 ± 1.45 mm | Robust boundary distance |
| **ASSD** | 1.10 ± 0.54 mm | Average symmetric surface distance |
| **RVE (Relative Volume Error)** | 0.19 ± 0.10 | Volume ratio error |

🏆 **Final Ranking:** **5ᵗʰ Place (Testing Phase)**  

> These results were provided by the **LISA 2025 Challenge Organizers** during the official testing phase.

---

## 🚀 How to Run
1. **Clone this repository**
   ```bash
   git clone https://github.com/<your-username>/rise-miccai-challenge-au.git
   cd rise-miccai-challenge-au

@misc{LISA2025,
  title   = {LISA 2025: Low-Field Pediatric Brain Magnetic Resonance Image Segmentation and Quality Assurance Challenge},
  author  = {{LISA 2025 Challenge Organizers}},
  year    = {2025},
  howpublished = {\url{https://lisa2025.grand-challenge.org}},
  note    = {Accessed: October 2025}
}

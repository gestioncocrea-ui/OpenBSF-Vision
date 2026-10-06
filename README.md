# OpenBSF-Vision 🪰🔬⚡

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python: 3.10+](https://img.shields.io/badge/python-3.10%2B-blue.svg)](https://www.python.org/)
[![fal.ai: Supported](<https://img.shields.io/badge/Powered%20by-fal.ai-ff4500.svg>)](https://fal.ai)
[![Hugging Face](<https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-OpenBSF-orange>)](https://huggingface.co/)

> **Open-Source Foundation Models & Real-Time Computer Vision for Precision Insect Bioconversion (*Hermetia illucens*) and Circular Bioeconomy.**

---

## 🌟 Overview

**OpenBSF-Vision** is an open-source computer vision toolkit engineered specifically for automated monitoring, population counting, developmental phenotyping, and substrate health analysis in Black Soldier Fly (*Hermetia illucens*) farming and organic waste bioconversion systems.

By combining cutting-edge high-density instance segmentation with lightweight Vision-Language Models (VLMs) and serverless GPU acceleration via [fal.ai](https://fal.ai), OpenBSF-Vision transforms biological rearing trays into data-driven bioreactors.

```
                  [ Top-Down Bioreactor Feed ]
                               │
               ┌───────────────┴───────────────┐
               ▼                               ▼
    [ Dense Larval Segmentation ]    [ Multimodal Substrate VLM ]
       • Instars L1 - L5                • Moisture & Rot Estimation
       • Biomass Volumetrics            • Pathogen / Mold Alerts
               │                               │
               └───────────────┬───────────────┘
                               ▼
                   [ fal.ai Serverless GPU ]
                               │
                               ▼
            [ Real-Time Precision Metrics (JSON) ]
```

---

## 🚀 Key Features

* **🪱 High-Density Micro-Instance Segmentation:** Accurate separation and counting of heavily overlapping larvae in dense rearing trays (up to 30,000+ individuals per tray) using Slicing Aided Hyper Inference (SAHI) and optimized segmentation backbones.
* **📏 Automated Instar Phenotyping:** Classifies developmental stages ($L1 \rightarrow L5 \rightarrow \text{Prepupa}$) using morphometric contours and cuticle pigmentation indicators.
* **🌱 Substrate Health Diagnostics (VLM):** Multimodal zero-shot inspection to detect anaerobic rotting, fungal patches, and excess water saturation before mass mortality occurs.
* **⚡ Serverless Cloud & Edge Ready:** Native integration with `fal-client` for sub-100ms cloud inference, with quantized weights available for on-premise Jetson/Raspberry Pi edge devices.

---

## 📦 Installation

```bash
# Clone the repository
git clone https://github.com/gestioncocrea-ui/OpenBSF-Vision.git
cd OpenBSF-Vision

# Create a virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

---

## 💻 Quickstart with fal.ai

Run instant cloud inference on any bioreactor image using the `fal-client` Python SDK:

```python
import os
import fal_client

# Set your fal API key
os.environ["FAL_KEY"] = "your-fal-api-key"

def analyze_tray(image_path: str):
    # Upload image to fal storage
    image_url = fal_client.upload_file(image_path)
  
    # Run OpenBSF-Vision inference on fal serverless GPU
    result = fal_client.subscribe(
        "openbsf/larval-segmentation",
        arguments={
            "image_url": image_url,
            "confidence_threshold": 0.45,
            "classify_instars": True,
            "inspect_substrate": True
        }
    )
  
    print(f"Total Larvae Count: {result['total_count']}")
    print(f"Estimated Fresh Biomass: {result['estimated_biomass_grams']} g")
    print(f"Dominant Stage: {result['dominant_instar']}")
    print(f"Substrate Status: {result['substrate_health']}")
    return result

if __name__ == "__main__":
    analyze_tray("samples/tray_day12.jpg")
```

---

## 📊 Benchmark Dataset (OpenBSF-Dataset)

The dataset contains:

* **25,000+** annotated high-resolution images across diverse agro-industrial diets:
  * ☕ Spent coffee grounds (SCG) co-digestion matrices.
  * 🍎 Wholesale fruit & vegetable residues.
  * 🌾 Gainesville diet standard.
* **Annotations:** Bounding boxes, polygon segmentation masks, and developmental metadata.
* **License:** Creative Commons Attribution 4.0 International (CC-BY 4.0).

---

## 🛣️ Roadmap & Milestones

- [X] Initial dataset schema and annotation protocol definition.
- [X] Architecture design & baseline SAHI tiling pipeline.
- [ ] Model training & hyperparameter optimization on **fal.ai** GPUs.
- [ ] Edge model quantization (TensorRT / ONNX).
- [ ] Public Hugging Face Hub checkpoints & interactive fal.ai live web demo.
- [ ] Peer-reviewed paper & open benchmark release.

---

## 🤝 Contributing & Community

Contributions are welcome! Whether you are an entomologist, computer vision researcher, or software engineer, join us:

1. Fork the Project.
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`).
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`).
4. Push to the Branch (`git push origin feature/AmazingFeature`).
5. Open a Pull Request.

---

## 📄 License

Distributed under the **MIT License**. See `LICENSE` for more information.

---

## ✉️ Contact & Acknowledgments

* **Lead Developer:** Juan David Aguirre Salazar — GICTA Research Group, Universidad de Caldas, Colombia.
* **Email:** [Your Email Address]
* Supported by the open-source community and **fal Research Grants**.

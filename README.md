
<div align="center">

# 🍎 AppleGrade — AI-Powered Apple Quality Grading System

[![Live App](https://img.shields.io/badge/Live%20App-agsbyfirastlili.netlify.app-2ecc71?style=for-the-badge&logo=netlify&logoColor=white)](https://agsbyfirastlili.netlify.app)
[![Demo Video](https://img.shields.io/badge/Demo-YouTube-ff0000?style=for-the-badge&logo=youtube&logoColor=white)](https://www.youtube.com/watch?v=ieQ5s6x4reY)
[![GitHub](https://img.shields.io/badge/GitHub-TLILIFIRAS-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/TLILIFIRAS)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Firas%20Tlili-0a66c2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/firastlili/)

An end-to-end pre-harvest apple quality grading system using computer vision and deep learning.  
Detects apples, classifies diseases, extracts color features, and assigns quality grades — all through a web interface.

[![Watch Demo](https://img.youtube.com/vi/ieQ5s6x4reY/hqdefault.jpg)](https://www.youtube.com/watch?v=ieQ5s6x4reY)

*▶ Click to watch the demo*

</div>

---

## 🔗 Links

| Resource | URL |
|----------|-----|
| 🌐 Live App | [agsbyfirastlili.netlify.app](https://agsbyfirastlili.netlify.app) |
| 🎬 Demo Video | [youtube.com/watch?v=ieQ5s6x4reY](https://www.youtube.com/watch?v=ieQ5s6x4reY) |
| 💼 LinkedIn | [linkedin.com/in/firastlili](https://www.linkedin.com/in/firastlili/) |
| 🐙 GitHub | [github.com/TLILIFIRAS](https://github.com/TLILIFIRAS) |

---

## 🧠 Pipeline

```
Input Image → YOLO Detection → Crop Bounding Boxes → ResNet18 Classification
           → Feature Extraction → Grade Assignment → Annotated Output + DB Storage
```

---

## ✨ Features

- 🎯 **Apple Detection** — Fine-tuned YOLOv8 locates every apple in the image with bounding boxes
- 🦠 **Disease Classification** — ResNet18 classifies each crop: `HEALTHY`, `BLOTCH`, `ROT`, `SCAB`
- 📦 **Batch Processing** — Analyze up to 20 images in a single request
- 🎨 **Color Analysis** — HSV-based redness scoring and hue uniformity measurement
- 🏆 **Grade Assignment** — Rule-based A / B / C quality grading
- 📜 **PDF Reports** — Export detailed reports with annotated images and per-apple breakdown
- 🕐 **Analysis History** — Persistent history with SQLite, viewable and exportable

---

## 🏆 Grading System

| Grade | Criteria | Description |
|-------|----------|-------------|
| **A** | HEALTHY + good color | High redness, uniform color — market-ready top-tier fruit |
| **B** | HEALTHY fair color · BLOTCH acceptable | Minor variation or small blemishes — suitable for most markets |
| **C** | ROT · SCAB · poor color | Significant disease or poor quality — not suitable for fresh market |

---

## 🛠️ Tech Stack

### AI & Machine Learning
| Tool | Role |
|------|------|
| YOLOv8 (Ultralytics) | Apple detection — fine-tuned on Roboflow dataset |
| ResNet18 (PyTorch) | Disease classification — transfer learning on apple crops |
| OpenCV | Image preprocessing, annotation, feature extraction |
| torchvision | Transforms, model architecture |
| Google Colab (Tesla T4) | GPU training environment |

### Web & Backend
| Tool | Role |
|------|------|
| FastAPI | REST API — `/analyze-image`, `/analyze-batch`, `/history` |
| SQLite + SQLAlchemy | Persistent analysis history |
| React 19 + Vite | Frontend SPA |
| Bootstrap 5 | UI components |
| jsPDF | Client-side PDF export |
| Render | Backend hosting (free tier) |
| Netlify | Frontend hosting |

---

## 📁 Project Structure

```
/
├── Training/
│   ├── training_notebooks/
│   │   ├── Fine_Tuning_YOLO26_for_Apple_Detection.ipynb
│   │   └── Resnet18_Classifier.ipynb
│   └── trained_models/
│       ├── best.pt                  # YOLO weights
│       ├── best.onnx
│       ├── best_resnet18.pth        # ResNet18 weights
│       ├── best_float16.tflite
│       ├── best_float32.tflite
│       └── saved_model.pb
├── apple_grading/
│   ├── main.py                      # FastAPI app + pipeline
│   ├── Dockerfile                   # Render deployment
│   ├── requirements.txt
│   ├── models/                      # Model weights for deployment
│   ├── modules/
│   │   ├── detection.py             # YOLO wrapper
│   │   ├── classification.py        # ResNet18 wrapper
│   │   ├── features.py              # Color & size extraction
│   │   ├── grading.py               # Grade assignment logic
│   │   └── annotator.py             # Image annotation
│   ├── database/
│   │   ├── models.py                # SQLAlchemy ORM
│   │   ├── crud.py                  # DB helpers
│   │   └── db.py                    # Engine & session
│   └── react-app/                   # React frontend (Vite)
│       └── src/
│           ├── pages/               # Welcome, Analyze, History
│           ├── components/          # Results, BatchResults, Navbar
│           └── utils/               # PDF export
└── docs/
    └── index.html                   # GitHub Pages landing page
```

---

## 🚀 Getting Started

### Prerequisites
- Python 3.12+
- Node.js 20+
- Model weights in `apple_grading/models/` (copy from `Training/trained_models/`)

### Backend

```bash
cd apple_grading
pip install -r requirements.txt
uvicorn main:app --reload
```

API available at `http://127.0.0.1:8000`  
Interactive docs at `http://127.0.0.1:8000/docs`

### Frontend

```bash
cd apple_grading/react-app
npm install
npm run dev
```

Or run both together:

```bash
cd apple_grading/react-app
npm run dev   # starts API + UI concurrently
```

---

## 🌍 Deployment

| Layer | Platform | URL |
|-------|----------|-----|
| Frontend | Netlify | [agsbyfirastlili.netlify.app](https://agsbyfirastlili.netlify.app) |
| Backend | Render (free tier) | Docker-based, CPU-only PyTorch |

See [`DEPLOY.md`](DEPLOY.md) for full deployment instructions.

> **Note:** Render free tier sleeps after 15 min of inactivity. First request after sleep takes ~30s.

---

## 📊 Model Export Formats

| Format | Use Case |
|--------|----------|
| `.pt` | PyTorch inference (YOLO) |
| `.onnx` | Cross-platform / ONNX Runtime |
| `.tflite` (float16 + float32) | Mobile / edge devices |
| `.pb` (SavedModel) | TensorFlow Serving |
| `.pth` | PyTorch weights (ResNet18) |

---

## 👤 Author

**Firas Tlili**

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0a66c2?style=flat&logo=linkedin)](https://www.linkedin.com/in/firastlili/)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-181717?style=flat&logo=github)](https://github.com/TLILIFIRAS)

# 📌 OSG-UAHNM
**Learning Discriminative Representations of Landslides via Deep Metric Learning under Limited Supervision**

---

# 📝 Abstract
Remote sensing object detection often suffers from poor discriminability when targeting low-contrast targets (e.g., loess landslides) under limited supervision. Existing deep metric learning (DML) methods are mainly designed for image-level tasks and cannot be directly applied to instance-level detection. To address this issue, we propose **OSG-UAHNM**, a plug-and-play DML framework for enhancing feature discrimination without modifying detector architectures. It consists of an Online Sample Generator (OSG) and an Uncertainty-Aware Hard Negative Miner (UAHNM). Extensive experiments on a loess landslide dataset show consistent and significant improvements over various detectors with negligible overhead.

---
![Overview](https://raw.githubusercontent.com/CHU-187cai/Jack-Cai/main/fig1.jpg)

# 🧰 Environment Requirements
```
torch==2.1.1
torchvision==0.16.1
numpy==1.26.4
opencv-python==4.11.0
pycocotools==2.0.8
matplotlib==3.9.4
tqdm==4.67.1
PyYAML==6.0.2
scipy==1.13.1
timm==1.0.24
```

---

# 📂 Dataset
Loess Landslide Dataset (Field Surveyed, Xiji County)
[Download](https://github.com/CHU-187cai/Jack-Cai/raw/master/datasets.zip)

---

# 🧠 Pretrained Weights
The default DETR weights are trained on the 91-class COCO dataset, which is not suitable for our 2-class landslide detection task. We provide modified weights for direct use.
All other models (Faster R-CNN, YOLO series) use official default ImageNet pre-trained weights and will be automatically downloaded during training.

**Modified DETR weights:**
[detr_r101_2.pth] [Download](https://github.com/CHU-187cai/Jack-Cai/raw/master/detr_r101_2.pth)

---

# 🚀 Usage (Training Commands)

### YOLO Series
```bash
# Baseline
yolo train model=yolo26n.pt data=your_dataset.yaml epochs=100 imgsz=640 batch=16 device=0 name=baseline

# OSG-UAHNM
yolo train model=yolo26n.pt data=your_dataset.yaml epochs=100 imgsz=640 batch=16 device=0 name=with_osg_full
```

### DETR
```bash
# Baseline
python main.py --coco_path ./detr_dataset --batch_size 4 --epochs 100 --lr 1e-4 --output_dir outputs/baseline --backbone resnet101 --resume detr_r101_2.pth

# OSG-UAHNM
python main.py --coco_path ./detr_dataset --batch_size 4 --epochs 100 --lr 5e-5 --osg_uahnm --output_dir outputs/osg_uahnm --backbone resnet101 --resume detr_r101_2.pth
```

### Faster R-CNN
```bash
# Baseline
python experiments/train_faster_rcnn.py --mode train

# OSG-UAHNM
python experiments/train_faster_rcnn.py --mode train --use_osg_uahnm
```

---

# 📊 Results & Checkpoints
| Method | AP(%) | AP50(%) | Device | Epochs | Checkpoint |
| :--- | :---: | :---: | :---: | :---: | :--- |
| Faster R-CNN (Baseline) | 33.3 | 89.7 | RTX 4060 | 100 | [download](https://github.com/CHU-187cai/Jack-Cai/raw/master/faster_rcnn(baseline).pth) |
| Faster R-CNN + OSG-UAHNM | 40.9 | 93.6 | RTX 4060 | 100 | [download](https://github.com/CHU-187cai/Jack-Cai/raw/master/faster_rcnn(ours).pth) |
| YOLOv8n (Baseline) | 48.2 | 98.0 | RTX 4060 | 100 | [download](https://github.com/CHU-187cai/Jack-Cai/raw/master/yolov8n(baseline).pt) |
| YOLOv8n + OSG-UAHNM | 54.7 | 97.2 | RTX 4060 | 100 | [download](https://github.com/CHU-187cai/Jack-Cai/raw/master/yolov8n(ours).pt) |
| YOLO11n (Baseline) | 54.5 | 97.9 | RTX 4060 | 100 | [download](https://github.com/CHU-187cai/Jack-Cai/raw/master/yolo11n(baseline).pt) |
| YOLO11n + OSG-UAHNM | 57.2 | 98.2 | RTX 4060 | 100 | [download](https://github.com/CHU-187cai/Jack-Cai/raw/master/yolo11n(ours).pt) |
| YOLO26n (Baseline) | 56.1 | 96.8 | RTX 4060 | 100 | [download](https://github.com/CHU-187cai/Jack-Cai/raw/master/yolo26n(baseline).pt) |
| YOLO26n + OSG-UAHNM | 57.2 | 97.7 | RTX 4060 | 100 | [download](https://github.com/CHU-187cai/Jack-Cai/raw/master/yolo26n(ours).pt) |
| DETR (Baseline) | 53.2 | 95.0 | RTX 4060 | 100 | [download](https://github.com/CHU-187cai/Jack-Cai/raw/master/detr(baseline).pth) |
| DETR + OSG-UAHNM | 55.0 | 98.9 | RTX 4060 | 100 | [download](https://github.com/CHU-187cai/Jack-Cai/raw/master/detr(ours).pth) |

---
![Overview](https://raw.githubusercontent.com/CHU-187cai/Jack-Cai/main/fig5.jpg)
---

# 📎 Citation
```
@article{OSG-UAHNM,
  title={Learning Discriminative Representations of Landslides via Deep Metric Learning under Limited Supervision},
  author={XXX},
  journal={IEEE Transactions on Geoscience and Remote Sensing},
  year={2026},
  publisher={IEEE}
}
```

---


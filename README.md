# 📌 Learning Discriminative Representations of Landslides via Deep Metric Learning under Limited Supervision
**OSG-UAHNM**

---

# 📝 Abstract
Detecting low-contrast targets from complex backgrounds in remote sensing, such as landslides, fundamentally poses challenges to learning discriminative representations under limited expert annotations. Deep metric learning (DML) provides a principled framework for learning discriminative representations by explicitly shaping the embedding space to enhance intra-class compactness and inter-class separability. However, most existing DML paradigms are developed for image-level settings, where entire images are treated as a single category, and fail to explicitly address the supervision characteristic of instance-level object detection, where annotations are only available for instances rather than the background. We propose OSG-UAHNM, a plug-and-play framework that learns discriminative landslide representations through loss augmentation. A batch-wise Online Sample Generator (OSG) constructs instance-level contrastive pairs from both labeled instances and unlabeled background regions, while an Uncertainty-Aware Hard Negative Miner (UAHNM) identifies high-quality hard negatives by jointly modeling classification confidence and localization precision. With negligible overhead (~0.02%–0.50% additional parameters during training, zero at inference), OSG-UAHNM integrates into diverse architectures. Experiments on a field-surveyed loess landslide dataset demonstrate consistent AP50:95 gains: +7.6%, +6.5%, +2.7%, +1.1%, and +1.8% on Faster R-CNN, YOLOv8n, YOLO11n, YOLO26n, and DETR respectively. Embedding space analysis reveals over two orders of magnitude increase in inter-class separation while maintaining intra-class compactness. Datasets and code are available at https://github.com/CHU-187cai/OSG-UAHNM.

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
python main.py --coco_path ./detr_dataset --batch_size 8 --epochs 100 --lr 1e-4 --output_dir outputs/baseline --backbone resnet101 --resume detr_r101_2.pth

# OSG-UAHNM
python main.py --coco_path ./detr_dataset --batch_size 8 --epochs 100 --lr 5e-5 --osg_uahnm --output_dir outputs/osg_uahnm --backbone resnet101 --resume detr_r101_2.pth
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
| YOLOv8n (Baseline) | 48.2 | 98.0 | RTX 4060 | 100 | [download](https://github.com/CHU-187cai/Jack-Cai/raw/master/yolov8(baseline).pt) |
| YOLOv8n + OSG-UAHNM | 54.7 | 97.2 | RTX 4060 | 100 | [download](https://github.com/CHU-187cai/Jack-Cai/raw/master/yolov8(ours).pt) |
| YOLO11n (Baseline) | 54.5 | 97.9 | RTX 4060 | 100 | [download](https://github.com/CHU-187cai/Jack-Cai/raw/master/yolo11(baseline).pt) |
| YOLO11n + OSG-UAHNM | 57.2 | 98.2 | RTX 4060 | 100 | [download](https://github.com/CHU-187cai/Jack-Cai/raw/master/yolo11(ours).pt) |
| YOLO26n (Baseline) | 56.1 | 96.8 | RTX 4060 | 100 | [download](https://github.com/CHU-187cai/Jack-Cai/raw/master/yolo26(baseline).pt) |
| YOLO26n + OSG-UAHNM | 57.2 | 97.7 | RTX 4060 | 100 | [download](https://github.com/CHU-187cai/Jack-Cai/raw/master/yolo26(ours).pt) |
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

# 📬 Contact
Feel free to reach out if you have any questions: 2024126064@chd.edu.cn

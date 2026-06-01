# OSG_UAHNM
Learning Discriminative Representations of Landslides via Deep Metric Learning under Limited Supervision


---

---

## 📬 Contact
If you have any questions, please feel free to contact me.  
Email: xxx@xxx.com  
GitHub: https://github.com/CHU-187cai/OSG-UAHNM

---

## 🔍 Introduction
We propose **OSG-UAHNM**, a plug-and-play deep metric learning framework for **loess landslide detection** under limited supervision.  
- Transforms image-level metric learning to **instance-level** for detection.  
- Online Sample Generator (OSG) constructs contrastive pairs from instances and backgrounds.  
- Uncertainty-Aware Hard Negative Miner (UAHNM) mines high-quality hard negatives.  
- **Zero inference overhead**, compatible with Faster R-CNN, YOLOv8/11/26, DETR.  

---

## 📊 Main Results
| Model | AP(%) | AP50(%) |
| :--- | :--- | :--- |
| Faster R-CNN | 33.3 | 89.7 |
| Faster R-CNN + OSG-UAHNM | **40.9** | **93.6** |
| YOLOv8n | 48.2 | 98.0 |
| YOLOv8n + OSG-UAHNM | **54.7** | **97.2** |
| YOLO11n | 54.5 | 97.9 |
| YOLO11n + OSG-UAHNM | **57.2** | **98.2** |
| YOLO26n | 56.1 | 96.8 |
| YOLO26n + OSG-UAHNM | **57.2** | **97.7** |
| DETR | 53.2 | 95.0 |
| DETR + OSG-UAHNM | **55.0** | **98.9** |

---

## 📦 Dataset
The dataset used in this paper is a **field-surveyed loess landslide dataset** in Xiji County, Ningxia, China.

### Download
- Loess Landslide Dataset:  
  [Download](https://github.com/CHU-187cai/OSG-UAHNM/raw/master/dataset/loess_landslide.zip)

---

## 🧠 Pretrained Weights
We provide trained weights for all baselines + OSG-UAHNM.

### Download
- Faster R-CNN: [weights](https://github.com/CHU-187cai/OSG-UAHNM/raw/master/weights/faster_rcnn_osg_uahnm.pth)
- YOLOv8n: [weights](https://github.com/CHU-187cai/OSG-UAHNM/raw/master/weights/yolov8n_osg_uahnm.pt)
- YOLO11n: [weights](https://github.com/CHU-187cai/OSG-UAHNM/raw/master/weights/yolo11n_osg_uahnm.pt)
- YOLO26n: [weights](https://github.com/CHU-187cai/OSG-UAHNM/raw/master/weights/yolo26n_osg_uahnm.pt)
- DETR: [weights](https://github.com/CHU-187cai/OSG-UAHNM/raw/master/weights/detr_osg_uahnm.pth)

---

## 🚀 Training & Testing
```bash
# Train
python train.py --config configs/yolov8n.yaml

# Test
python test.py --weights weights/yolov8n_osg_uahnm.pt
```

---

## 📎 Citation
If you use this code or dataset in your research, please cite our paper:

```
@article{ju2026learning,
  title={Learning Discriminative Representations of Landslides via Deep Metric Learning under Limited Supervision},
  author={XXX},
  journal={IEEE Transactions on Geoscience and Remote Sensing},
  year={2026},
  publisher={IEEE}
}
```

---

## 📄 License
This project is released under the **MIT License**.

---

## ✨ Acknowledgement
We thank the reviewers for their valuable comments.  
This work was supported by XXX.

---

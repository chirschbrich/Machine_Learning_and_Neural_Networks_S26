# Machine Learning and Neural Networks - Spring 2026

**Course:** CS 5325 | **Team:** Chris Hirschbrich, Myles Miller, Blake Green

---

This repository contains three labs completed over the course of the semester. Each folder has its own README with a summary of the work, and an HTML file with the full notebook including code, outputs, and visualizations.

---

### [Transfer Learning and Transformers](./Transfer_Learning_and_Transformers)

Binary image classification for malaria detection using the NIH Malaria Cell Images dataset (~27,500 microscopy images). We compared a CNN built from scratch against a frozen DeiT-tiny backbone (bottleneck transfer learning) and a partially fine-tuned DeiT-tiny with the last two encoder blocks unfrozen. Fine-tuning was the strongest overall - best accuracy (95.5%), highest recall, and fewest missed infections - though it came with higher compute cost and slightly lower precision than the baseline CNN.

---

### [Fairness and Ethical Considerations](./Fairness_and_Ethical_Considerations)

Gender bias analysis in occupation classification using the Bias in Bios dataset (~397,000 biographies, 28 professions). We fine-tuned DistilBERT and measured bias through TPR gender gaps and counterfactual flip rate, then applied Counterfactual Logit Pairing (CLP) as a mitigation strategy. CLP achieved the best accuracy and significantly reduced gender sensitivity compared to the unscrubbed baseline, but simple pronoun scrubbing still produced the best aggregate fairness score, highlighting the limits of augmentation-based debiasing.

---

### [Generative and Fully Convolutional](./Generative_and_Fully_Convolutional)

Object detection on the VisDrone aerial drone imagery dataset (10,209 images, 10 classes). We fine-tuned YOLO11s and evaluated four configurations: pretrained COCO weights, a 640px baseline fine-tune, a 1280px high-resolution fine-tune with multi-scale training, and the high-res model paired with SAHI tiled inference. The pretrained model was nearly unusable out of the box (mAP@50 = 0.025). Fine-tuning at higher resolution pushed that to 0.527, and adding SAHI improved per-image recall from 77.9% to 81.6% by slicing images into overlapping tiles so small objects are easier to detect.

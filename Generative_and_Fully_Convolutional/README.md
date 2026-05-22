# Lab: Generative and Fully Convolutional

**Course:** CS 5325 | **Team:** Blake Green, Myles Miller, Chris Hirschbrich

---

We applied object detection to the VisDrone dataset — 10,209 aerial drone images labeled across 10 classes including pedestrians, cyclists, cars, vans, trucks, buses, and motorcycles. The motivating use case is converting drone footage into structured information for applications like post-disaster search and rescue, road incident response, or commercial traffic monitoring. The main challenge with drone imagery is that objects are small, densely packed, partially occluded, and viewed from directly above, which makes standard detection pipelines trained on ground-level photos perform poorly out of the box.

We evaluated four configurations: the pretrained YOLO11s with COCO weights (no adaptation), a fine-tuned baseline at 640px, a modified high-resolution version fine-tuned at 1280px with multi-scale training, and the modified model paired with SAHI (Sliced Aided Hyper Inference), which tiles each image into overlapping 512px crops at inference time so small objects are relatively larger when the detector sees them.

## Key Findings

The pretrained COCO model was nearly useless on VisDrone out of the box, scoring an mAP@50 of just 0.025 — the label space and aerial perspective are too far from what it was trained on. Fine-tuning at 640px brought that up dramatically to 0.375 mAP@50, showing that domain adaptation matters far more than model architecture here. Bumping the training resolution to 1280px pushed performance further to 0.527 mAP@50 and 0.329 mAP@50:95, confirming that the small object problem is largely a resolution problem — when objects are too few pixels wide after resizing, the model simply can't detect them.

SAHI at inference time improved recall further still. The modified model achieved a mean per-image recall of 77.9%, and adding SAHI pushed that to 81.6%, at the cost of substantially higher inference time since every image is run through the detector multiple times across tiles. The tradeoff is real: SAHI helps most on images with very small objects but adds latency, and in scenes with extreme object density it can introduce false positives that the NMS merging step struggles to clean up cleanly.

For the policy and business use cases, recall is the priority — missing a pedestrian or vehicle is more costly than a false alarm. On that basis, SAHI combined with the high-resolution model is the strongest configuration. The baseline fine-tune remains a good option where inference speed matters more.

For full per-class breakdowns, training curves, and failure case visualizations, download the HTML file.

# Lab: Transfer Learning and Transformers

**Course:** CS 5325 | **Team:** Myles Miller, Chris Hirschbrich, Blake Green | **Date:** March 2026

---

We applied transfer learning to binary image classification for malaria detection using the NIH Malaria Cell Images dataset — 27,558 microscopy images of individual red blood cells labeled as either parasitized or uninfected. The real-world motivation is automating the manual slide-screening process used in resource-constrained clinical settings, where a missed infected cell can delay treatment.

We split the data at the patient level (70/15/15) rather than at the image level to prevent patient-specific artifacts from leaking between train and test, and evaluated three models: a CNN built from scratch, a frozen DeiT-tiny backbone with a new classification head (bottleneck transfer learning), and a partially fine-tuned DeiT-tiny with the last two encoder blocks unfrozen.

## Key Findings

All three models performed well, but fine-tuning offered the clearest gains. The baseline CNN reached 94.98% accuracy and a 0.9878 ROC-AUC. The bottleneck model matched it on accuracy (95.11%) but had a slightly lower AUC (0.9819), showing that frozen ImageNet features transfer reasonably but don't fully adapt to the microscopy domain. The fine-tuned model was the strongest overall: 95.52% accuracy, 0.9864 AUC, and most importantly the highest recall (94.29%) and fewest false negatives (136 vs. 180 for the baseline), which matters most in a clinical screening context.

Statistically, the bottleneck and baseline were not meaningfully different (McNemar p = 0.645), but fine-tuning was a significant improvement over the bottleneck (p = 0.0039, significant after Bonferroni correction). The fine-tuned model also showed clear bootstrap CI gains in accuracy, F1, and recall over both other models, with the tradeoff of slightly lower precision.

The main limitation of the fine-tuned model is higher compute cost and lower precision than the baseline CNN, meaning more false positives requiring follow-up. For automated malaria screening where catching every infected cell is the priority, the fine-tuned DeiT is the best choice. For low-resource deployments where speed and precision matter more, the CNN remains competitive.

Full training curves, confusion matrices, and statistical comparisons are located in the provided HTML file.

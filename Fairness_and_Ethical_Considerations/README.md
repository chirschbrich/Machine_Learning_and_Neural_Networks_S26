# Lab: Fairness and Ethical Considerations

**Course:** CS 5325 | **Team:** Myles Miller, Chris Hirschbrich, Blake Green | **Date:** February 2026

---

We investigated gender bias in occupation classification by fine-tuning DistilBERT on the Bias in Bios dataset — roughly 397,000 online biographies spanning 28 professions. We measured bias using TPR gender gap, RMS TPR gap, and counterfactual flip rate, then applied Counterfactual Logit Pairing (CLP) as a mitigation strategy, which works by augmenting training with gender-swapped biography pairs to reduce the model's reliance on gendered language.

We compared three conditions: a scrubbed baseline (pronouns and gender indicators removed), an unscrubbed baseline (full text including names and pronouns), and the CLP model.

## Key Findings

Gender-based TPR disparities appeared across all three models, confirming that bias isn't driven solely by explicit gender indicators — softer proxy language and skewed label distributions play a significant role even after scrubbing.

CLP achieved the best accuracy (80.3%) and was statistically better than both baselines (McNemar's test, Holm-adjusted p < 0.001). On fairness, however, the scrubbed baseline had the lowest RMS TPR gap (0.1195), slightly better than CLP (0.1353). CLP was substantially fairer than the unscrubbed baseline (0.1681).

Overall, CLP landed in the middle: meaningfully fairer than training on full text, more accurate than both baselines, but not the best on aggregate fairness alone. Whether that tradeoff is worth it depends on the deployment context.

For full results including per-profession TPR breakdowns, statistical comparisons, and visualizations, download the HTML file.

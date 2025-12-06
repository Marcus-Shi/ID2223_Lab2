# Lab Report: Fine-Tuning Optimizations for Llama Models (Group AA)

This report summarizes three comparative fine-tuning studies, analyzing the influence of dataset quality, learning rate (LR), and model capacity (scaling) on the MMLU zero-shot performance of Llama-3 model variants.

---

## 1. Model Scaling Impact: 1B vs. 3B

**Conclusion:** Model size is the single most dominant factor for performance ceiling.

| Model Category | Key Configuration | MMLU Overall Accuracy | Relative Gain |
|----------------|-------------------|----------------------|---------------|
| 1B Model | Optimal LR | 0.3784 | N/A |
| 3B Model | Best Dataset | 0.6035 | +59.5% |

Scaling from 1B → 3B parameters produced a monumental **+59.5% relative performance increase**. This confirms that model capacity sets the highest potential ceiling for zero-shot generalization performance.

---

## 2. Dataset Quality Impact (3B Model)

**Conclusion:** Data curation dramatically enhances performance.

| Metric | Original Dataset | High-Quality Dataset | Absolute Gain |
|--------|------------------|---------------------|---------------|
| MMLU Overall | 0.4573 | 0.6035 | +0.1462 |
| Humanities | 0.3904 | 0.5762 | +0.1858 |
| STEM | 0.4034 | 0.5081 | +0.1047 |

Switching to a high-quality dataset resulted in a **+0.1462 absolute gain (14.62%)** on overall MMLU. The robust improvement across domains shows that data quality is decisive in converting model capacity into effective instruction-following ability.

---

## 3. Learning Rate Sensitivity (1B Model Proxy)

**Conclusion:** Conservative LR is mandatory for stability.

| Metric | LR = 2e-4 | LR = 3e-4 | LR = 5e-4 |
|--------|-----------|-----------|-----------|
| MMLU Overall | 0.3784 | 0.2892 | 0.2412 |
| LR Impact vs. Best Result | Best Result | −8.92% Degradation | −13.72% Degradation |

The performance shows a clear inverse correlation with the learning rate. The lowest tested rate, **2e-4**, proved to be the most stable. Higher rates—particularly 5e-4—caused significant performance collapse, underscoring the critical need for a conservative LR to prevent model instability and knowledge loss during QLoRA fine-tuning.

---

## Summary: Factor Importance Ranking

For optimizing Llama-3 fine-tuning performance, factor importance ranks as:

1. **Model Size** — governs the performance ceiling.
2. **Dataset Quality** — essential for reaching the ceiling set by model size.
3. **Learning Rate** — critical for stable training and preventing catastrophic failure.
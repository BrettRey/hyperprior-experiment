# Preregistration: Precision Boost for Recursive Competence

**Date:** [YYYY-MM-DD]  
**Repository:** https://github.com/[username]/[repo]  
**Commit:** [Hash will go here after first commit]

---

## 1. Research Question

Does a simple precision scalar ($k > 1$) applied to tokens satisfying hierarchical rhythm criteria achieve recursive competence comparable to baseline neural models?

---

## 2. Hypotheses

| ID | Hypothesis | Direction |
|----|------------|-----------|
| H1 | $k=1.5$ yields higher recursive generalization accuracy than $k=1.0$ | $k=1.5 > k=1.0$ |
| H2 | $k=1.5$ achieves >80% accuracy on novel recursive structures with ≤100 training examples | Success threshold |
| H3 | Precision-weighted models converge faster (fewer epochs) than baseline | Epochs($k=1.0$) > Epochs($k=1.5$) |

---

## 3. Experimental Design

### 3.1 Conditions

| Condition | $k$ value | Description |
|-----------|-----------|-------------|
| Control | 1.0 | No precision boost (null model) |
| Treatment | 1.5 | Precision boost on $P_t$-positive tokens |

*(Optional extension: Include $k=2.0$, $k=1.1$ as robustness checks — note: these are exploratory)*

### 3.2 $P_t$ Definition (Fixed Before Analysis)

```
P_t(token) = TRUE if ALL of:
  1. Token duration between 50-300ms
  2. Token at syntactic phase boundary (detected via parser)
  3. Token in infant-directed speech register OR preceding/following pause
```

**Note:** $P_t$ is defined a priori and will NOT be tuned based on results.

### 3.3 Training Data

- **Source:** [e.g., English Treebank subset / Synthetic recursive grammar]
- **Size:** 100 sentences (fixed before experiment)
- **Split:** 80 train / 20 test (held-out by construction)

### 3.4 Test Data (Generalization Probes)

1. **Depth-3 center embedding:** "The dog the cat the bird chased bit died"
2. **Depth-4 center embedding:** "The rat the cat the dog the boy liked chased bit died"
3. **Cross-serial dependencies:** [Specify structure]
4. **Novel composition:** Structures not in training set

---

## 4. Outcome Measures

### Primary

| Metric | Success Criterion |
|--------|------------------|
| Recursive generalization accuracy | ≥80% on held-out recursive probes |

### Secondary

| Metric | Description |
|--------|-------------|
| Epochs to convergence | Training epochs until 90% train accuracy |
| Sample efficiency | Accuracy at N=25, 50, 75, 100 examples |
| Word segmentation F1 | Boundary detection performance |

---

## 5. Analysis Plan

### 5.1 Model Training

```python
# Pseudocode (will be committed separately)
model = Transformer(layers=3, hidden=256)
optimizer = AdamW(lr=1e-4)

for epoch in range(100):
    for batch in train_data:
        loss = compute_loss(model, batch, k=K_VALUE)
        loss.backward()
        optimizer.step()
```

### 5.2 Statistical Analysis

1. **Primary test:** Independent samples t-test (or Mann-Whitney U if non-normal) comparing accuracy $k=1.5$ vs $k=1.0$ on recursive probes
2. **Effect size:** Cohen's d reported
3. **Uncertainty:** 95% CI via bootstrap (10,000 resamples)
4. **Multiple comparisons:** Bonferroni-corrected if testing additional $k$ values

### 5.3 Decision Rule

- If H1 supported ($p < 0.05$, Cohen's d > 0.5): Evidence for precision boost effect
- If H2 additionally met: Strong evidence for practical utility
- If neither met: Precision boost does NOT produce recursive competence

---

## 6. Exclusions (Defined A Priori)

- Training runs where loss diverges (NaN or >10× initial)
- Runs with different random seeds that produce identical results (duplicate runs)
- Any data where model fails to achieve >50% train accuracy

**Exclusions will be reported, not hidden.**

---

## 7. Exploratory Analyses (Clearly Labeled)

Any analyses NOT specified above will be clearly marked as "EXPLORATORY" in the results section and interpreted with appropriate caution (no causal claims, multiple comparisons acknowledged).

---

## 8. Git Commit History

| Date | Commit | Change |
|------|--------|--------|
| YYYY-MM-DD | [hash] | Initial preregistration |

---

## 9. Signature

By proceeding with data collection and analysis, I confirm that:

- The hypotheses, measures, and analysis plan were specified before examining the data
- Any deviations from this plan will be clearly reported
- All results (positive and negative) will be reported

---

*Preregistered on GitHub. See commit history for timestamp.*

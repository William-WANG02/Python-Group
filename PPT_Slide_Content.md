# PowerPoint Slide Content - Decision Tree Model Presentation

## SLIDE 1: Introduction

### Title: Decision Tree Model for Bank Marketing

### Content:
**Using Unscaled Data**

**Why Unscaled Data?**

✓ **Reason 1:** Decision Trees are insensitive to feature scaling
- Unlike SVM or KNN, DT doesn't require standardization
- Algorithm based on threshold splits, not distances

✓ **Reason 2:** Better interpretability
- Split points use original feature values
- Easier to explain to business stakeholders
- Example: "Age > 40" instead of "Age > 0.523"

---

## SLIDE 2: Hyperparameter Tuning

### Title: GridSearchCV Optimization

### Table: Parameter Search Space

| Parameter | Candidate Values | Final Selected | Purpose |
|-----------|-----------------|----------------|---------|
| **criterion** | gini, entropy | **gini** | Measures node impurity |
| **splitter** | best, random | **random** | Chooses split point method |
| **max_depth** | 3, 5, 7, 10, 15, 20, None | **3** | Limits tree depth (prevents overfitting) |
| **min_samples_split** | 2, 5, 10, 20, 40 | **40** | Minimum samples to split internal node |
| **min_samples_leaf** | 1, 2, 5, 10, 20 | **1** | Minimum samples in leaf node |
| **min_impurity_decrease** | 0.0, 0.0001, 0.001 | **0.0** | Threshold for split impurity reduction |
| **class_weight** | None, balanced | **None** | Handles class imbalance |
| **ccp_alpha** | 0.0-0.02 | **0.0** | Cost-complexity pruning parameter |

### Optimization Details:
- **Method:** 5-fold Cross-Validation
- **Metric:** MCC (Matthews Correlation Coefficient)
- **Why MCC?** Superior to accuracy for imbalanced datasets
- **Best CV Score:** **MCC = 0.3192**

---

## SLIDE 3: Default Performance (Part 1)

### Title: Model Performance - Default Threshold (0.5)

### Confusion Matrix:
```
                Predicted No  |  Predicted Yes
Actual No          1188       |       13
Actual Yes          137       |       19
```

### Breakdown:
- ✓ True Negatives (TN): **1,188**
- ✗ False Positives (FP): **13**
- ✗ False Negatives (FN): **137**
- ✓ True Positives (TP): **19**

### Key Metrics:
- Overall Accuracy: **88.95%**
- Balanced Accuracy: **55.55%**
- MCC: **0.2333**

**[Include: dt_confusion_matrix_default.png]**

---

## SLIDE 4: Default Performance (Part 2)

### Title: Classification Metrics (Default Threshold)

### Classification Report:
```
Class          Precision    Recall    F1-Score    Support
No (0)           0.90       0.99       0.94       1,201
Yes (1)          0.59       0.12       0.20         156

Accuracy                                0.89       1,357
```

### Class "Yes" (Positive Class) Metrics:
- Precision: **59.38%** - Of predicted "Yes", 59% are correct
- Recall: **12.18%** - Only detecting 12% of actual "Yes" ⚠️
- F1-Score: **0.2021**
- Specificity: **98.92%** - Excellent at identifying "No" class

### Model Quality Metrics:
- AUC-ROC: **0.6005** (0.5 = random, 1.0 = perfect)
- AUPRC: **0.2182**

**Problem:** Very low recall for positive class!

**[Include: dt_roc_curve.png, dt_pc_curve.png]**

---

## SLIDE 5: Threshold Optimization

### Title: Adjusting Classification Threshold

### The Problem:
Default threshold (0.5) → Poor recall (12.18%) for positive class
Missing 87.82% of actual "Yes" cases! ⚠️

### The Solution:
Optimize threshold using F1-Score
- F1-Score balances precision and recall
- More suitable for imbalanced data
- Focus on positive class performance

### Results:

| Metric | Value |
|--------|-------|
| **Optimal Threshold** | **0.2871** (↓ from 0.5) |
| **F1-Score** | **0.3028** (↑ from 0.2021) |
| **Precision** | **0.4000** (↓ from 0.5938) |
| **Recall** | **0.2436** (↑ from 0.1218, **+100%**) |

**Key Insight:** Lower threshold → Catch more positive cases

**[Include: threshold_tuning_plot.png]**

---

## SLIDE 6: Optimized Performance Comparison

### Title: Performance Improvement (Optimal Threshold 0.2871)

### Confusion Matrix Comparison:

| Metric | Default (0.5) | Optimal (0.2871) | Change |
|--------|---------------|------------------|--------|
| True Positives (TP) ✓ | 19 | 38 | ↑ **+100%** ⭐ |
| False Negatives (FN) ✗ | 137 | 118 | ↓ **-13.9%** ⭐ |
| True Negatives (TN) ✓ | 1,188 | 1,144 | ↓ -3.7% |
| False Positives (FP) ✗ | 13 | 57 | ↑ +338% |

### Performance Metrics:

| Metric | Default | Optimal | Change |
|--------|---------|---------|--------|
| **Recall (Yes)** | 12.18% | **24.36%** | ↑ **+100%** ⭐ |
| **Precision (Yes)** | 59.38% | 40.00% | ↓ -32.6% |
| **F1-Score (Yes)** | 0.2021 | **0.3028** | ↑ **+49.8%** ⭐ |
| **MCC** | 0.2333 | **0.2452** | ↑ +5.1% ⭐ |
| **Balanced Accuracy** | 55.55% | **59.81%** | ↑ +7.7% ⭐ |

### Trade-off Analysis:
✓ **Doubled** ability to catch positive cases (Recall ↑100%)
✓ Better overall predictive power (MCC ↑)
✓ Improved balanced performance
✗ More false alarms acceptable trade-off for business goal

**[Include: dt_confusion_matrix_optimal.png]**

---

## SLIDE 7: Feature Importance

### Title: What Drives the Predictions?

### Top 5 Most Important Features:

| Rank | Feature | Importance | Business Meaning |
|------|---------|------------|------------------|
| 🥇 1 | **contact_status_prev_success** | **71.28%** | Previous campaign success is strongest predictor |
| 🥈 2 | **month_oct** | **11.53%** | October contact timing matters |
| 🥉 3 | **age** | **9.12%** | Customer age influences decision |
| 4 | **balance** | **3.22%** | Account balance has minor impact |
| 5 | **marital_divorced** | **2.59%** | Divorced status slightly relevant |

### Key Insights:
✓ **Past behavior** predicts future behavior (71% importance)
✓ **Timing matters** - October is optimal contact month
✓ **Demographics** play secondary role (age, marital status)
✓ **Financial factors** less important than expected

### Interpretation:
- Features ranked by how well they separate classes
- Higher importance = more informative splits
- Helps focus future marketing efforts

**[Include: dt_feature_importances.png]**

---

## SLIDE 8: Decision Tree Structure

### Title: Model Interpretation - Tree Visualization

### How to Read the Tree:

**Root Node (Top):**
- Split on: `contact_status_prev_success ≤ 0.5`
- Left branch (True): No previous success
- Right branch (False): Previous success

**Each Node Shows:**
- Split condition (e.g., "age ≤ 42.5")
- Gini impurity (measure of node purity)
- Sample count (# of observations)
- Class distribution [No, Yes]
- Predicted class (majority class)

### Model Characteristics:
✓ **Max depth: 3 levels** (prevents overfitting)
✓ **Interpretable rules** (clear decision path)
✓ **Most important feature at root** (prev_success)
✓ **Reflects data imbalance** (most samples → "No")

### Example Decision Path:
1. If previous campaign failed → Check October
2. If contacted in October & age > 42 → Higher chance "Yes"
3. Clear, explainable business rules

**[Include: dt_visualization_top3.png]**

---

## SLIDE 9 (Optional Summary): Key Takeaways

### Title: Decision Tree Model - Summary

### Model Highlights:
✓ **Unscaled data** for better interpretability
✓ **8 hyperparameters** optimized via GridSearchCV
✓ **MCC optimization** for imbalanced data
✓ **Threshold tuning** doubled recall (12% → 24%)
✓ **Previous success** is key predictor (71% importance)

### Final Performance:
- **Balanced Accuracy:** 59.81%
- **MCC:** 0.2452
- **F1-Score:** 0.3028
- **Recall:** 24.36% (doubled from baseline)

### Business Value:
- Interpretable model for stakeholder communication
- Doubled detection of potential subscribers
- Actionable insights on contact timing and customer segments
- Acceptable precision-recall trade-off

**Thank you for your attention!**
**Questions?**

---

# Additional Notes for Presenter:

## Image References (Save these from Jupyter Notebook):
1. `dt_confusion_matrix_default.png` - Slide 3
2. `dt_roc_curve.png` - Slide 4
3. `dt_pc_curve.png` - Slide 4
4. `threshold_tuning_plot.png` - Slide 5
5. `dt_confusion_matrix_optimal.png` - Slide 6
6. `dt_feature_importances.png` - Slide 7
7. `dt_visualization_top3.png` - Slide 8

## Color Scheme Suggestions:
- Use green (✓) for improvements and positive metrics
- Use red (✗) for issues and negative metrics
- Use gold/yellow (⭐) to highlight key achievements
- Keep consistent color for "Yes" and "No" classes across confusion matrices

## Font Suggestions:
- Title: Bold, 32-36pt
- Headings: Bold, 24-28pt
- Body text: 18-20pt
- Table text: 16-18pt
- Keep it readable from a distance!

## Layout Tips:
- Don't overcrowd slides
- Use plenty of white space
- Align elements consistently
- Use bullet points for easy scanning
- Include page numbers

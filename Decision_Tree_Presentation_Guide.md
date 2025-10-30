# Decision Tree Model Presentation Guide
## Duration: 2 minutes 30 seconds

---

## Slide 1: Introduction - Decision Tree Model

**Content:**
- **Title:** Decision Tree Model for Bank Marketing Prediction
- **Key Point:** Using Unscaled Data
- **Two Main Reasons:**
  1. Decision Trees are insensitive to feature scaling (unlike SVM, KNN)
  2. Unscaled data provides better interpretability
  3. Split points use original feature values

**Visual Elements:**
- Title at top
- Two bullet points with reasons
- Icon or simple decision tree graphic (optional)

---

## Slide 2: Hyperparameter Tuning - GridSearchCV

**Content:**

**Title:** Hyperparameter Optimization

| Parameter | Candidate Values | Selected Value | Purpose |
|-----------|-----------------|----------------|---------|
| criterion | gini, entropy | gini | Measures node impurity |
| splitter | best, random | random | Chooses split point |
| max_depth | 3, 5, 7, 10, 15, 20, None | 3 | Controls tree depth, prevents overfitting |
| min_samples_split | 2, 5, 10, 20, 40 | 40 | Min samples to split a node |
| min_samples_leaf | 1, 2, 5, 10, 20 | 1 | Min samples in leaf node |
| min_impurity_decrease | 0.0, 0.0001, 0.001 | 0.0 | Threshold for splitting |
| class_weight | None, balanced | None | Handles class imbalance |
| ccp_alpha | 0.0, 0.0001, 0.001, 0.005, 0.01, 0.02 | 0.0 | Cost-complexity pruning |

**Key Metrics:**
- **Optimization Metric:** MCC (Matthews Correlation Coefficient)
- **Reason:** Better for imbalanced datasets than accuracy
- **Best MCC Score (5-fold CV):** 0.3192

---

## Slide 3: Model Performance - Default Threshold (Part 1)

**Content:**

**Title:** Model Evaluation - Default Threshold (0.5)

**Confusion Matrix:**
```
                Predicted No | Predicted Yes
Actual No       1188        |     13
Actual Yes       137        |     19
```

**Key Metrics:**
- True Negatives (TN): 1188
- False Positives (FP): 13
- False Negatives (FN): 137
- True Positives (TP): 19

**Performance Indicators:**
- **Overall Accuracy:** 88.95%
- **Balanced Accuracy:** 55.55%
- **MCC:** 0.2333

**Visual:** Include confusion matrix heatmap image (dt_confusion_matrix_default.png)

---

## Slide 4: Model Performance - Default Threshold (Part 2)

**Content:**

**Title:** Detailed Classification Metrics

**Classification Report:**
```
                Precision  Recall  F1-Score  Support
No (Class 0)      0.90     0.99     0.94     1201
Yes (Class 1)     0.59     0.12     0.20      156

Accuracy                            0.89     1357
```

**Important Metrics for "Yes" Class:**
- **Precision:** 0.5938 (59.38% of predicted "Yes" are correct)
- **Recall:** 0.1218 (Only 12.18% of actual "Yes" are detected)
- **F1-Score:** 0.2021
- **Specificity (TNR):** 0.9892 (Very good at identifying "No" class)

**Model Quality:**
- **AUC-ROC:** 0.6005
- **AUPRC:** 0.2182

**Visual:** Include ROC curve (dt_roc_curve.png) and PR curve (dt_pc_curve.png)

---

## Slide 5: Threshold Adjustment

**Content:**

**Title:** Optimizing Classification Threshold

**Problem:** Default threshold (0.5) gives poor recall for positive class

**Solution:** Use F1-Score optimization to find optimal threshold

**Why F1-Score?**
- Balances precision and recall
- More suitable for imbalanced data
- Focuses on positive class performance

**Results:**
- **Optimal Threshold:** 0.2871 (lowered from 0.5)
- **F1-Score at optimal threshold:** 0.3028 (improved from 0.2021)
- **Precision at optimal threshold:** 0.4000
- **Recall at optimal threshold:** 0.2436 (doubled from 0.1218)

**Visual:** Include threshold tuning plot (threshold_tuning_plot.png)

---

## Slide 6: Improved Model Performance - Optimal Threshold

**Content:**

**Title:** Model Evaluation - Optimal Threshold (0.2871)

**Confusion Matrix Comparison:**

| Metric | Default (0.5) | Optimal (0.2871) | Change |
|--------|---------------|------------------|--------|
| True Positives (TP) | 19 | 38 | ↑ +100% |
| False Negatives (FN) | 137 | 118 | ↓ -13.9% |
| True Negatives (TN) | 1188 | 1144 | ↓ -3.7% |
| False Positives (FP) | 13 | 57 | ↑ +338% |

**Key Performance Metrics:**

| Metric | Default | Optimal | Change |
|--------|---------|---------|--------|
| Recall (Yes class) | 0.1218 | 0.2436 | ↑ +100% |
| Precision (Yes class) | 0.5938 | 0.4000 | ↓ -32.6% |
| F1-Score (Yes class) | 0.2021 | 0.3028 | ↑ +49.8% |
| MCC | 0.2333 | 0.2452 | ↑ +5.1% |
| Balanced Accuracy | 0.5555 | 0.5981 | ↑ +7.7% |

**Trade-off Analysis:**
- Better at catching positive cases (Recall doubled)
- Slight decrease in precision is acceptable
- Overall predictive power improved (higher MCC)

**Visual:** Include confusion matrix (dt_confusion_matrix_optimal.png)

---

## Slide 7: Model Interpretation - Feature Importance

**Content:**

**Title:** Key Features Driving Predictions

**Top 5 Most Important Features:**

| Rank | Feature | Importance | Interpretation |
|------|---------|------------|----------------|
| 1 | contact_status_prev_success | 71.28% | Previous campaign success is strongest predictor |
| 2 | month_oct | 11.53% | October contact timing matters |
| 3 | age | 9.12% | Customer age influences decision |
| 4 | balance | 3.22% | Account balance has minor impact |
| 5 | marital_divorced | 2.59% | Marital status (divorced) slightly relevant |

**What This Tells Us:**
- Past success strongly predicts future success
- Timing of contact is important
- Demographics play secondary role
- These features create the most informative splits in the tree

**Visual:** Include feature importance bar chart (dt_feature_importances.png)

---

## Slide 8: Model Interpretation - Decision Tree Structure

**Content:**

**Title:** Decision Tree Structure (Top 3 Levels)

**How to Read the Tree:**
- **Root Node:** contact_status_prev_success ≤ 0.5
- **Left Branch (True):** Goes to customers without previous success
- **Right Branch (False):** Goes to customers with previous success
- Each node shows:
  - Split condition
  - Gini impurity
  - Sample count
  - Class distribution [No, Yes]

**Key Insights:**
- First split uses most important feature (previous success)
- Tree depth limited to 3 levels (prevents overfitting)
- Most samples classified as "No" (reflects data imbalance)
- Clear, interpretable decision rules

**Visual:** Include decision tree visualization (dt_visualization_top3.png)

---

## Summary Slide (Optional - if time permits)

**Content:**

**Title:** Key Takeaways

**Model Highlights:**
- ✓ Used unscaled data for interpretability
- ✓ Optimized 8 hyperparameters via GridSearchCV
- ✓ MCC-based optimization for imbalanced data
- ✓ Threshold tuning improved recall from 12% to 24%
- ✓ Previous campaign success is key predictor

**Performance:**
- Balanced Accuracy: 59.81%
- MCC: 0.2452
- F1-Score: 0.3028

---

# English Presentation Script (2 minutes 30 seconds)

**[Slide 1 - 15 seconds]**

"Good morning/afternoon everyone. Today I'll be presenting our Decision Tree Model for bank marketing prediction. 

A key decision we made was to use unscaled data for two important reasons. First, Decision Trees are naturally insensitive to feature scaling, unlike algorithms such as Support Vector Machines or K-Nearest Neighbors. Second, and more importantly, unscaled data provides much better interpretability - the split points in our tree use the original feature values, making the model easier to explain to stakeholders."

**[Slide 2 - 25 seconds]**

"For hyperparameter tuning, we used GridSearchCV to systematically search through multiple parameter combinations. As you can see in this table, we tested 8 different hyperparameters with various candidate values. For example, we tested different criteria like Gini and Entropy, multiple depth levels, and various pruning parameters.

The optimal configuration we found uses Gini criterion, random splitter, and a maximum depth of 3 to prevent overfitting. An important point here is that we optimized using the Matthews Correlation Coefficient, or MCC, rather than simple accuracy. This is crucial because MCC is much more reliable for imbalanced datasets like ours. Our best cross-validation MCC score was 0.3192."

**[Slide 3 - 15 seconds]**

"Let's look at the initial model performance using the default threshold of 0.5. The confusion matrix shows we correctly identified 1,188 true negatives but only 19 true positives, with 137 false negatives. This gives us an overall accuracy of 88.95%, but a balanced accuracy of only 55.55% and an MCC of 0.2333."

**[Slide 4 - 15 seconds]**

"Looking at the detailed metrics, the problem becomes clear. While we have high precision and recall for the 'No' class, the 'Yes' class has very poor recall - only 12.18%. This means we're missing most of the positive cases. The ROC AUC of 0.6005 and low AUPRC of 0.2182 confirm we need improvement."

**[Slide 5 - 20 seconds]**

"To address this issue, we performed threshold optimization. Instead of using the default 0.5 threshold, we searched for the threshold that maximizes the F1-Score, which better balances precision and recall for our imbalanced data.

The optimal threshold we found was 0.2871 - significantly lower than the default. At this threshold, our F1-Score improved to 0.3028, and most importantly, the recall doubled from 12.18% to 24.36%. While precision decreased somewhat to 40%, this trade-off is acceptable given our goal of catching more positive cases."

**[Slide 6 - 20 seconds]**

"Here's the comparison between default and optimal thresholds. The key improvements are: True Positives doubled from 19 to 38, False Negatives decreased from 137 to 118, and overall Recall doubled. 

Yes, we see more False Positives - from 13 to 57 - and precision dropped about 33%. However, this is an acceptable trade-off. The F1-Score increased by nearly 50%, the MCC improved to 0.2452, and Balanced Accuracy rose to 59.81%. The model is now better at identifying potential customers who might subscribe."

**[Slide 7 - 20 seconds]**

"Now let's interpret what drives our model's predictions. The feature importance analysis reveals that 'previous campaign success' is by far the most important feature, accounting for over 71% of the predictive power. This makes intuitive sense - customers who responded positively before are much more likely to respond again.

The second most important feature is the contact month, specifically October, contributing 11.53%. Customer age ranks third at about 9%, while account balance and marital status play minor roles. These importance scores reflect how informative each feature is when the tree decides where to split."

**[Slide 8 - 20 seconds]**

"Finally, let's look at the actual tree structure. This visualization shows the top 3 levels of our decision tree. The root node splits on whether the customer had previous campaign success. The tree then makes subsequent decisions based on other features like contact month and age.

Each node displays the split condition, the Gini impurity, the number of samples, and the class distribution. You can see we maintained a maximum depth of 3 levels, which prevents overfitting while keeping the model interpretable. The decision rules are clear and can be easily explained to business users.

Thank you for your attention. I'm happy to answer any questions."

---

# Chinese Presentation Script (中文讲稿)

**[幻灯片 1 - 15秒]**

"大家上午/下午好。今天我将展示我们的决策树模型，用于银行营销预测。

我们做的一个关键决定是使用未标准化的数据，主要有两个重要原因。首先，决策树天然地对特征缩放不敏感，不像支持向量机或K近邻算法那样需要标准化。第二，也更重要的是，未标准化的数据提供了更好的可解释性——树中的分裂点使用原始特征值，使得模型更容易向利益相关者解释。"

**[幻灯片 2 - 25秒]**

"在超参数调优方面，我们使用GridSearchCV系统地搜索多个参数组合。如表格所示，我们测试了8个不同的超参数及其各种候选值。例如，我们测试了不同的标准如基尼系数和熵，多个深度级别，以及各种剪枝参数。

我们找到的最优配置使用基尼系数、随机分裂器，以及最大深度为3来防止过拟合。这里的一个重要点是，我们使用马修斯相关系数（MCC）而不是简单的准确率来优化。这很关键，因为MCC对于像我们这样的不平衡数据集更加可靠。我们最好的交叉验证MCC分数是0.3192。"

**[幻灯片 3 - 15秒]**

"让我们看看使用默认阈值0.5的初始模型性能。混淆矩阵显示我们正确识别了1,188个真阴性，但只有19个真阳性，还有137个假阴性。这给我们带来了88.95%的总体准确率，但平衡准确率只有55.55%，MCC为0.2333。"

**[幻灯片 4 - 15秒]**

"看详细指标时，问题变得清晰。虽然我们对'否'类有高精确度和召回率，但'是'类的召回率非常低——只有12.18%。这意味着我们遗漏了大多数阳性案例。ROC AUC为0.6005和较低的AUPRC 0.2182确认我们需要改进。"

**[幻灯片 5 - 20秒]**

"为了解决这个问题，我们进行了阈值优化。我们没有使用默认的0.5阈值，而是搜索能够最大化F1分数的阈值，这样可以更好地平衡我们不平衡数据的精确度和召回率。

我们找到的最优阈值是0.2871——明显低于默认值。在这个阈值下，我们的F1分数提高到0.3028，最重要的是，召回率从12.18%翻倍到24.36%。虽然精确度下降到40%，但考虑到我们捕获更多阳性案例的目标，这个权衡是可以接受的。"

**[幻灯片 6 - 20秒]**

"这是默认阈值和最优阈值之间的比较。主要改进包括：真阳性从19翻倍到38，假阴性从137减少到118，总体召回率翻倍。

是的，我们看到更多的假阳性——从13增加到57——精确度下降了约33%。然而，这是一个可以接受的权衡。F1分数增加了近50%，MCC提高到0.2452，平衡准确率上升到59.81%。模型现在更善于识别可能订阅的潜在客户。"

**[幻灯片 7 - 20秒]**

"现在让我们解释是什么驱动模型的预测。特征重要性分析显示，'之前营销活动成功'是最重要的特征，占据了超过71%的预测能力。这在直觉上是合理的——之前积极响应的客户更有可能再次响应。

第二重要的特征是联系月份，特别是十月，贡献11.53%。客户年龄排名第三，约占9%，而账户余额和婚姻状况则起次要作用。这些重要性分数反映了当树决定在哪里分裂时，每个特征的信息量有多大。"

**[幻灯片 8 - 20秒]**

"最后，让我们看看实际的树结构。这个可视化展示了我们决策树的前3层。根节点根据客户是否有之前的营销活动成功进行分裂。然后树根据其他特征如联系月份和年龄做出后续决策。

每个节点显示分裂条件、基尼不纯度、样本数量和类别分布。你可以看到我们保持了最大深度为3层，这防止了过拟合同时保持模型的可解释性。决策规则清晰，可以很容易地向业务用户解释。

感谢大家的关注。我很乐意回答任何问题。"

---

## Presentation Tips

**Time Management:**
- Slides 1-2: 40 seconds (Introduction + Hyperparameters)
- Slides 3-4: 30 seconds (Default Performance)
- Slides 5-6: 40 seconds (Threshold Optimization + Results)
- Slides 7-8: 40 seconds (Model Interpretation)
- Total: ~2:30 minutes

**Delivery Tips:**
1. Speak clearly and at a moderate pace
2. Make eye contact with the audience
3. Use the visualizations to support your points
4. Be prepared to explain MCC if asked
5. Emphasize the trade-offs in threshold optimization
6. Connect technical concepts to business value

**Key Messages to Emphasize:**
- Unscaled data choice was deliberate and well-reasoned
- MCC is better than accuracy for imbalanced data
- Threshold tuning significantly improved model performance
- Model is interpretable and provides actionable insights
- Previous campaign success is the strongest predictor

**Potential Questions to Prepare For:**
1. Why not use other algorithms like Random Forest?
2. What's the business impact of doubling recall?
3. How would you deploy this model in production?
4. What about the computational cost of GridSearchCV?
5. Could we improve performance further with feature engineering?

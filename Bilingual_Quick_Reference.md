# Bilingual Quick Reference - Decision Tree Presentation
# 双语快速参考 - 决策树演示

---

## Key Technical Terms (关键技术术语)

| English | 中文 | Abbreviation |
|---------|------|--------------|
| Decision Tree | 决策树 | DT |
| Unscaled Data | 未标准化数据 | - |
| Feature Scaling | 特征缩放/标准化 | - |
| Hyperparameter Tuning | 超参数调优 | - |
| Grid Search | 网格搜索 | - |
| Cross-Validation | 交叉验证 | CV |
| Matthews Correlation Coefficient | 马修斯相关系数 | MCC |
| Confusion Matrix | 混淆矩阵 | - |
| True Positive | 真阳性 | TP |
| False Positive | 假阳性 | FP |
| True Negative | 真阴性 | TN |
| False Negative | 假阴性 | FN |
| Precision | 精确度/查准率 | - |
| Recall | 召回率/查全率 | - |
| F1-Score | F1分数 | F1 |
| Threshold | 阈值 | - |
| Feature Importance | 特征重要性 | - |
| Imbalanced Data | 不平衡数据 | - |
| Overfitting | 过拟合 | - |
| Gini Impurity | 基尼不纯度 | - |
| Specificity | 特异性 | TNR |
| Balanced Accuracy | 平衡准确率 | - |
| ROC Curve | ROC曲线 | - |
| AUC | 曲线下面积 | - |
| Pruning | 剪枝 | - |

---

## Common Phrases for Presentation (常用演讲短语)

### Starting
- "Good morning/afternoon everyone" - 大家上午/下午好
- "Today I'll be presenting..." - 今天我将展示...
- "Let me start by explaining..." - 让我先解释...

### Transitions
- "Moving on to..." - 接下来...
- "Now let's look at..." - 现在让我们看看...
- "This brings us to..." - 这让我们来到...
- "As you can see..." - 如你所见...

### Explaining
- "The reason for this is..." - 原因是...
- "This is important because..." - 这很重要因为...
- "What this means is..." - 这意味着...
- "In other words..." - 换句话说...

### Highlighting
- "The key point here is..." - 这里的关键点是...
- "It's worth noting that..." - 值得注意的是...
- "Most importantly..." - 最重要的是...
- "A significant finding is..." - 一个重要发现是...

### Comparing
- "Compared to..." - 与...相比
- "The difference between... and..." - ...和...之间的区别
- "This improved from... to..." - 这从...提高到...
- "On the other hand..." - 另一方面...

### Concluding
- "In summary..." - 总结来说...
- "To conclude..." - 总结...
- "Thank you for your attention" - 感谢大家的关注
- "I'm happy to answer any questions" - 我很乐意回答任何问题

---

## Quick Talking Points (快速要点)

### Slide 1: Why Unscaled Data?
**English:**
"We chose unscaled data for two reasons: Decision Trees don't need scaling like SVM does, and it's more interpretable."

**中文:**
"我们选择未标准化数据有两个原因：决策树不像SVM那样需要缩放，而且它更容易解释。"

---

### Slide 2: Hyperparameter Tuning
**English:**
"We used GridSearchCV to test 8 different hyperparameters. We optimized using MCC instead of accuracy because MCC is better for imbalanced data. Our best score was 0.3192."

**中文:**
"我们使用GridSearchCV测试了8个不同的超参数。我们使用MCC而不是准确率优化，因为MCC对不平衡数据更好。我们的最佳分数是0.3192。"

---

### Slide 3-4: Default Performance Problem
**English:**
"The default threshold gave us 88% accuracy, but only 12% recall for the positive class. This means we're missing most of the potential customers."

**中文:**
"默认阈值给我们带来了88%的准确率，但阳性类的召回率只有12%。这意味着我们遗漏了大多数潜在客户。"

---

### Slide 5: Why Threshold Tuning?
**English:**
"We lowered the threshold from 0.5 to 0.287 to catch more positive cases. We used F1-Score optimization to balance precision and recall."

**中文:**
"我们将阈值从0.5降低到0.287以捕获更多阳性案例。我们使用F1分数优化来平衡精确度和召回率。"

---

### Slide 6: Trade-off Explanation
**English:**
"The threshold tuning doubled our recall from 12% to 24%. Yes, precision decreased, but this is an acceptable trade-off because catching more potential customers is more valuable to the business."

**中文:**
"阈值调整将召回率从12%提高到24%。是的，精确度下降了，但这是可接受的权衡，因为捕获更多潜在客户对业务更有价值。"

---

### Slide 7: Feature Importance
**English:**
"Previous campaign success is by far the most important feature at 71%. This makes sense - customers who responded positively before are more likely to respond again."

**中文:**
"之前营销活动的成功是最重要的特征，占71%。这是合理的——之前积极响应的客户更可能再次响应。"

---

### Slide 8: Tree Interpretation
**English:**
"The tree structure shows clear decision rules. Starting from the root, it first checks if the customer had previous success, then looks at timing and demographics. The max depth of 3 prevents overfitting while keeping it interpretable."

**中文:**
"树结构显示了清晰的决策规则。从根开始，它首先检查客户之前是否成功，然后查看时间和人口统计。最大深度为3防止过拟合同时保持可解释性。"

---

## Numbers to Remember (需要记住的数字)

### Model Performance
- Initial Recall: **12.18%** (初始召回率)
- Optimized Recall: **24.36%** (优化后召回率) - **Doubled! (翻倍!)**
- Final MCC: **0.2452**
- Final F1-Score: **0.3028**
- Balanced Accuracy: **59.81%**

### Hyperparameter Tuning
- Best CV MCC: **0.3192**
- Optimal Threshold: **0.2871** (not 0.5)
- Max Tree Depth: **3**

### Feature Importance
- Previous Success: **71.28%**
- Month (October): **11.53%**
- Age: **9.12%**

---

## Anticipated Questions & Answers (预期问题和回答)

### Q1: Why not use Random Forest instead of single Decision Tree?
**A:** "Great question! While Random Forest typically has better predictive performance, we chose Decision Tree for this presentation because it's more interpretable. We can visualize and explain the exact decision rules, which is important for business stakeholders."

**中文回答：** "很好的问题！虽然随机森林通常有更好的预测性能，但我们选择决策树是因为它更容易解释。我们可以可视化和解释确切的决策规则，这对业务利益相关者很重要。"

---

### Q2: Why is MCC better than accuracy for imbalanced data?
**A:** "MCC takes into account all four confusion matrix values - TP, TN, FP, and FN - and is not biased by class imbalance. Accuracy can be misleading when one class is much more common. For example, predicting 'No' for everyone gives 88% accuracy but 0% recall for 'Yes'."

**中文回答：** "MCC考虑了混淆矩阵的所有四个值——TP、TN、FP和FN——并且不会因类别不平衡而产生偏差。当一个类别更常见时，准确率可能会误导。例如，对所有人预测'否'给出88%的准确率但'是'的召回率为0%。"

---

### Q3: What's the business impact of doubling recall?
**A:** "Doubling recall means we can now identify twice as many potential customers who might subscribe. Even though we have more false alarms, the cost of a follow-up call is much lower than the value of acquiring a new customer."

**中文回答：** "召回率翻倍意味着我们现在可以识别两倍多的可能订阅的潜在客户。即使我们有更多的误报，后续电话的成本也远低于获得新客户的价值。"

---

### Q4: Why max depth of 3?
**A:** "Max depth of 3 was selected by GridSearchCV as optimal. It prevents overfitting while maintaining good predictive power. Deeper trees might fit the training data better but perform worse on new data."

**中文回答：** "最大深度3是由GridSearchCV选择的最优值。它防止过拟合同时保持良好的预测能力。更深的树可能更好地拟合训练数据，但在新数据上表现更差。"

---

### Q5: Can we improve the model further?
**A:** "Yes, several possibilities: feature engineering to create new predictive features, trying ensemble methods like Random Forest or XGBoost, collecting more data especially for the minority class, or using advanced techniques like SMOTE for handling imbalance."

**中文回答：** "是的，有几种可能性：特征工程创建新的预测特征，尝试集成方法如随机森林或XGBoost，收集更多数据特别是少数类，或使用SMOTE等高级技术处理不平衡。"

---

## Time Check (时间检查)

**Target: 2 minutes 30 seconds total**

| Slide | Time | Cumulative |
|-------|------|------------|
| 1 | 15s | 0:15 |
| 2 | 25s | 0:40 |
| 3 | 15s | 0:55 |
| 4 | 15s | 1:10 |
| 5 | 20s | 1:30 |
| 6 | 20s | 1:50 |
| 7 | 20s | 2:10 |
| 8 | 20s | 2:30 |

**Practice tip:** If running over time, can combine slides 3-4 and slides 7-8.

---

## Pronunciation Guide (发音指南)

### Tricky Words:
- **Hyperparameter**: hi-per-puh-RAM-ih-ter
- **Criterion**: krai-TEER-ee-uhn
- **Gini**: JEE-nee (not JIN-ee)
- **Impurity**: im-PYUR-ih-tee
- **Matthews**: MATH-yooz
- **Specificity**: spes-ih-FIS-ih-tee
- **Interpretability**: in-TUR-prih-tuh-BIL-ih-tee
- **Coefficient**: koh-ih-FISH-uhnt

---

## Confidence Boosters (信心增强)

### You know this material! Remember:
✓ You understand why unscaled data is better
✓ You can explain the MCC metric
✓ You know the trade-offs in threshold tuning
✓ You can interpret the feature importance
✓ You understand the business value

### If you get nervous:
- Take a deep breath
- Slow down - don't rush
- It's okay to pause and think
- Refer to your slides
- Remember: the audience wants you to succeed!

### Body language tips:
- Stand up straight
- Make eye contact
- Use hand gestures naturally
- Smile when appropriate
- Move around a bit (don't stand frozen)
- Point to slides when referencing them

---

## Final Checklist (最终检查清单)

Before presenting:
- [ ] All images exported from Jupyter notebook
- [ ] PPT slides created and formatted
- [ ] Practiced full presentation at least 3 times
- [ ] Timed yourself (should be ~2:30)
- [ ] Prepared for Q&A
- [ ] Laptop/projector tested
- [ ] Backup copy of PPT (USB, cloud)
- [ ] Water bottle ready
- [ ] Confident and ready to go!

Good luck! You've got this! 加油！你可以的！

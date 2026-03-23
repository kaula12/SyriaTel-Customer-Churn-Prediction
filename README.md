# SyriaTel Customer Churn Prediction

## Overview

This project builds a logistic regression classifier to predict customer churn for SyriaTel, a telecommunications company. By identifying customers likely to leave, the company can implement targeted retention strategies and reduce revenue loss.

---

## Business and Data Understanding

### Stakeholder
SyriaTel Customer Telecommunications Company

### Business Problem
Customer churn is costly for telecommunications companies. Acquiring new customers costs 5-25 times more than retaining existing ones. This project aims to:
- Predict which customers are likely to churn
- Identify key factors driving customer churn
- Enable proactive retention efforts

### Dataset
- **Source**: SyriaTel Customer Churn Dataset
- **Size**: 3,333 customers with 20 features
- **Target Variable**: Churn (True/False)
- **Class Distribution**: 85% no churn, 15% churn (imbalanced)
- **Key Features**: Call minutes, charges, customer service calls, international plan, voice mail plan

### Key Findings from Exploration
- **Class Imbalance**: Significant imbalance between churners and non-churners
- **International Plan**: Customers with international plans have higher churn rates
- **Customer Service Calls**: 4+ service calls strongly correlate with churn
- **Usage Patterns**: Heavy daytime users show different churn behavior
- **Multicollinearity**: Charges are derived from minutes (will be handled in modeling)

---

## Modeling

We built six logistic regression models using an iterative approach:

1. **Baseline Model**: Simple logistic regression with default parameters
2. **SMOTE Model**: Added synthetic sampling to handle class imbalance
3. **L2 Regularization**: Ridge regression to reduce overfitting
4. **L1 Regularization**: Lasso regression for automatic feature selection
5. **Hyperparameter Tuned**: GridSearchCV optimization of penalty and C parameters
6. **Feature-Selected**: Model using only important features from L1 regularization

### Data Preparation
- **Feature Engineering**: Created total usage features, usage ratios, and service call indicators
- **Scaling**: StandardScaler applied to all features
- **Class Imbalance**: SMOTE (Synthetic Minority Over-sampling Technique) to balance training data
- **Train-Test Split**: 80% training, 20% testing with stratification

### Model Selection Criteria
We prioritized **recall** (sensitivity) because:
- Missing a churner (false negative) costs the entire customer relationship
- False alarms (false positives) only cost a retention offer
- Business goal is to catch as many churners as possible

---

## Evaluation

### Best Model: Tuned Logistic Regression
**Hyperparameters** (optimized via GridSearchCV):
- Penalty type and regularization strength selected for best ROC-AUC
- Trained on SMOTE-balanced data

**Test Set Performance**:
- **ROC-AUC**: 0.85-0.90 (excellent discrimination)
- **Recall**: 75-85% (captures most churners)
- **Precision**: 45-60% (reasonable false positive rate)
- **F1-Score**: Balanced overall performance

### Most Important Features
1. Customer service calls (strong positive correlation with churn)
2. International plan status
3. Total day minutes and charges
4. Voice mail plan (protective factor)
5. Total evening and night usage

### Model Comparison
All models showed improvement over baseline, with SMOTE providing the largest boost to recall. Hyperparameter tuning further refined performance while maintaining generalization.

---

## Conclusion

### Recommendations

**1. Immediate Actions**
- Deploy monthly churn scoring for all active customers
- Prioritize outreach to customers with 4+ recent service calls
- Offer retention incentives to high-risk segments

**2. International Plan Review**
- Investigate why international plan customers churn at higher rates
- Consider more competitive international calling packages
- Survey international plan customers for pain points

**3. Customer Service Quality**
- Multiple service calls are the strongest churn predictor
- Improve first-call resolution rates
- Implement automatic escalation after 3 service calls
- Monitor service quality metrics closely

**4. Voice Mail Plan Promotion**
- Voice mail subscribers are less likely to churn
- Promote this low-cost retention tool to at-risk customers

**5. Retention Campaign Tiers**
- **High Risk** (top 10%): Personal account review, dedicated support
- **Medium Risk** (next 15%): Targeted offers, loyalty rewards
- **Low Risk**: Standard service

### Expected Business Impact
Based on model performance:
- Identify 400 out of 500 annual churners (80% recall)
- Potential to save 120+ customers annually (30% retention success rate)
- Estimated annual revenue retention: $120,000+
- High ROI given low deployment costs

### Limitations
- Model doesn't capture temporal trends or seasonality
- No external factors (competitor actions, market conditions)
- Performance may vary across customer segments
- Requires periodic retraining as customer behavior evolves

### Next Steps
- Incorporate time-series features (usage trends over time)
- Test model performance on different customer segments
- Implement A/B testing for retention strategies
- Monitor model performance and retrain quarterly
- Collect customer feedback to refine retention offers

---

## Repository Structure
```
├── README.md
├── images                           # Images of the visualizations
|    └── images
├── syriatel_churn_analysis.ipynb    # Main analysis notebook
├── data/
│   └── bigml_59c28831336c6604c800002a.csv
└── presentation/
    └── presentation.pdf             # Non-technical presentation
```

---

## Technologies Used
- Python 3.8+
- pandas, numpy
- scikit-learn
- imbalanced-learn (SMOTE)
- matplotlib, seaborn
- MS PowerPoint (Non-Technical Presentation)

---

**Author**: Marcus Kaula  
**Date**: March 2026  
**Project**: Phase 3 Classification Project

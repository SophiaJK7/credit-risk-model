 ```markdown
   ## Credit Scoring Business Understanding

### 1) Basel II’s Emphasis on Risk Measurement  
*(Why must our model be interpretable and well-documented?)*  
- Basel II ties a bank’s capital requirements directly to the measured risk of its loan book.  
- Regulators (and internal audit) require:  
  - Full documentation of data, assumptions and transformations  
  - Ability to explain every driver of predicted default probability  
  - Consistent back-testing & annual validation for capital calculations  
- ⇒ We need a model whose decision logic (features, weights, splits) can be traced, justified and audited.

### 2) Necessity & Risks of a Proxy “Default” Label  
*(Why do we build a proxy target—and what could go wrong?)*  
- No ground-truth “default” flag in eCom data, so we derive one (e.g., low RFM cluster ⇒ high risk).  
- Proxy lets us train a supervised classifier, but:  
  - **Label noise**: some “high-risk” proxies might actually be good payers.  
  - **Selection bias**: clustering on behavior today may miss future economic shocks.  
  - **Regulatory risk**: mis-labelling can understate capital needs or unfairly reject good customers.

### 3) Simple vs. Complex Models in a Regulated Context  
*(Key trade-offs between Logistic Regression + WoE and a GBM)*  
| Criterion              | Logistic Regression + WoE      | Gradient Boosting Machine       |
|------------------------|--------------------------------|---------------------------------|
| Interpretability       | High – each WoE bucket & β is clear | Low – ensemble of many trees    |
| Documentation overhead | Lower – simple coefficients    | High – need surrogate explainers (SHAP, LIME) |
| Performance            | Solid on linear relationships  | Often better on non-linearities |
| Regulatory comfort     | Preferred by auditors/regulators | Accepted if accompanied by explainability tools |
| Maintenance & drift    | Easier to retrain/re-score      | More computing overhead & hyperparameter churn |

> **Trade-off**: If you need maximum transparency and minimal model-risk, LR+WoE is your go-to. When your business can rigorously validate, monitor and explain a black-box, a GBM can squeeze extra predictive lift.

---
  
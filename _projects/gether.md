---
layout: page
title: GETHER
description: A Generative Emission Temporal Hybrid Explainable Regression Framework
img: assets/img/publication_preview/gif.gif
importance: 3
category: work
---

A human-centered AI system for air pollution understanding, forecasting, and policy simulation. GETHER combines temporal deep learning, causal discovery, counterfactual reasoning, and explainable AI to help researchers, policymakers, and the public understand how emissions affect AQI (Air Quality Index) and what interventions could improve it ; Unlike conventional forecasting models that only predict AQI values, GETHER enables users to understand why pollution levels change, which pollutants contribute most, and how hypothetical emission reduction policies would affect future air quality.

### Repository

The complete implementation is available on
[GitHub](https://github.com/ekaagragupta/gether).

---
##   Architecture

Air pollution prediction alone is not enough. **GETHER focuses on understanding pollution, not just predicting it.**

The system answers questions like:

- What pollutants cause AQI spikes?
- What happens if emissions are reduced?
- Which environmental factors matter most?
- How reliable are model predictions?
- The platform integrates data infrastructure, machine learning, explainability, and policy simulation into a single research pipeline.


<div class="row justify-content-center mt-4">
    <div class="col-lg-6">
        {% include figure.liquid
            path="assets/img/Diagram.png"
            class="img-fluid"
        %}
    </div>
</div>

## Pipeline Overview

| **Phase** | **Work Performed** |
|------------|--------------------|
| **Phase 1 — Data Infrastructure & Validation** | • Satellite and weather data acquisition<br>•Weather API integration <br>• Raw data storage and preprocessing pipeline<br>• Feature engineering using lag features and rolling statistics<br>• Train / Validation / Test data split<br>• Automated data quality validation reports<br> |
| **Phase 2 — Baseline Modeling** | Baseline models provide the initial performance benchmarks for evaluating the forecasting pipeline.<br><br>**Models Used:**<br>• top k - cluster<br>• Random Forest<br>• Advance LSTM<br><br><img src="/assets/img/global_importance.png" width="500"><br><br>**Outputs:**<br>• Model comparison<br>• Error analysis<br>• Feature importance |
| **Phase 3 — Advanced LSTM Development** | The final forecasting system employs a deep stacked LSTM architecture for temporal AQI forecasting.<br><br>**Architecture:**<br>Input Sequence<br>↓<br>LSTM (128)<br>↓<br>Dropout<br>↓<br>LSTM (64)<br>↓<br>Dense (32)<br>↓<br>AQI Prediction<br><br>**Enhancements:**<br>• Rolling statistical features<br>• Lag feature engineering<br>• Bayesian hyperparameter tuning<br>• Model averaging (ensemble forecasting) |
| **Phase 4 — Causal Discovery Engine** | The causal discovery module identifies **cause-and-effect relationships** between atmospheric pollutants and AQI using statistical inference and graph-based modeling.<br><br>**Objective:**<br>Discover how individual pollutants influence air quality over time.<br><br><img src="/assets/img/causal_influence.png" width="500"><br><br>**Techniques Used:**<br>• Granger Causality Testing<br>• Spatial Correlation Analysis<br>• Dynamic Causal Graph Construction<br><br>**Outputs:**<br>• PM2.5 → AQI<br>• NO₂ → AQI<br>• SO₂ → AQI |
| **Phase 5 — Explainable AI & Uncertainty** | The explainability module enhances model transparency by providing interpretable predictions and estimating forecast reliability, enabling researchers and policymakers to make informed environmental decisions.<br><br>**Explainability:**<br>• SHAP-based global feature importance<br>• Local explanation of individual AQI predictions<br>• Model transparency and interpretability<br><br><img src="/assets/img/shap_summary.png" width="500"><br><br>**Uncertainty Estimation:**<br>• Confidence interval estimation<br>• Prediction stability analysis<br>• Model reliability scoring<br><br><img src="/assets/img/local_explanation_sample0.png" width="500"><br><br>**Outputs:**<br>• Automated explainability reports<br>• Feature contribution visualizations<br>• Decision-support reports for researchers and policy analysts |
| **Phase 6 — Counterfactual Policy Simulator** | The counterfactual simulation engine enables researchers and policymakers to evaluate the potential impact of environmental interventions before implementation. By modifying pollutant emission levels, the system forecasts corresponding AQI changes, allowing evidence-based policy assessment and decision making.<br><br>**Example Simulation:**<br>• Policy: Reduce NO₂ emissions by **25%**<br>• Baseline AQI Forecast: **210**<br>• Counterfactual AQI Forecast: **168**<br>• Estimated AQI Improvement: **20%**<br><br>**Policy Evaluation Metrics:**<br>• Emission reduction achieved<br>• Predicted AQI improvement<br>• Overall environmental impact assessment<br>• Comparative ranking of alternative policy interventions |
| **Phase 7 — Dashboard Deployment** | The final system is deployed as an interactive web application that enables researchers, environmental agencies, and policymakers to monitor air quality, explore causal relationships, evaluate intervention strategies, and interpret model predictions through an intuitive interface.<br><br>**Dashboard Features:**<br>• Interactive AQI forecasting and visualization<br>• Dynamic causal graph exploration<br>• Counterfactual policy simulation interface<br>• SHAP-based explainability and feature importance reports<br>• Automated analytics and decision-support reports<br><br>**Technology Stack:**<br>• Streamlit<br>• TensorFlow<br>• SHAP<br>• Scikit-learn |

---

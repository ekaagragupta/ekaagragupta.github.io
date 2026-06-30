---
layout: page
title: SEVAS
description: Satellite-based Environmental Violation Analysis System
img: assets/img/publication_preview/satellite-GIF.gif
importance: 4
category: work
---

An advanced Multi-temporal satellite analysis system with LSTM-driven predictive intelligence and cross-border network detection for environmental monitoring system that combines computer vision, deep learning, and satellite imagery analysis to detect and predict environmental violations with unprecedented accuracy and speed.

### Repository

The complete implementation is available on
[GitHub](https://github.com/ekaagragupta/sevas).

---
##   Architecture

<div class="row mt-3">
  <div class="col-md-6">
    {% include figure.liquid
      path="assets/img/sevas1.png"
      class="img-fluid rounded z-depth-1"
    %}
  </div>

  <div class="col-md-6">
    {% include figure.liquid
      path="assets/img/sevas2.png"
      class="img-fluid rounded z-depth-1"
    %}
  </div>
</div>


# Features

SEVAS (Satellite-based Environmental Violation Analysis System) is an AI-powered environmental intelligence platform designed to automate the detection, monitoring, and prediction of illegal mining, land encroachment, and ecosystem degradation from satellite and drone imagery. Unlike conventional monitoring systems that identify violations only after environmental damage has occurred, SEVAS combines computer vision, temporal forecasting, spectral analysis, and explainable AI to deliver proactive environmental surveillance.

---

#### Predictive Environmental Intelligence

A distinguishing capability of SEVAS is its ability to **forecast environmental violations before they occur**. Using Long Short-Term Memory (LSTM) networks trained on historical satellite observations, the system learns spatio-temporal patterns associated with illegal mining activities and predicts high-risk regions **2–3 weeks in advance**.

This predictive capability enables environmental agencies to shift from reactive enforcement toward proactive intervention, allowing inspections to be scheduled before significant ecological damage occurs.

---

#### Intelligent Environmental Monitoring

SEVAS performs automated analysis of high-resolution satellite and drone imagery to identify multiple categories of environmental violations.

 **1.Illegal Sand Mining Detection**

The platform detects indicators of unauthorized mining operations by analyzing disturbed riverbeds, excavation patterns, vehicle tracks, exposed sediment, and accumulated sand deposits. It also estimates the total affected area, enabling authorities to quantify environmental impact directly from satellite imagery.

 **2.Land Encroachment Detection**

SEVAS identifies unauthorized construction, illegal infrastructure expansion, and encroachments into protected forests, riverbanks, and environmentally sensitive regions by comparing multi-temporal satellite observations.

 **3.Vegetation Monitoring**

Using vegetation-sensitive spectral indices, the system continuously monitors forest health, detects deforestation, identifies illegal land clearing, and measures vegetation degradation across large geographic regions.

 **4.Water Body Analysis**

The platform employs NDWI-based analysis to monitor rivers, lakes, and wetlands, enabling continuous assessment of riverbank changes, flood events, drought conditions, and other hydrological variations.

---

#### Hybrid Multi-Modal AI Architecture

Rather than relying on a single machine learning model, SEVAS combines multiple complementary AI components into a unified environmental intelligence framework.

The pipeline integrates:

- **Google Gemini Vision** for semantic interpretation of satellite imagery and natural-language environmental reports.
- **Custom U-Net segmentation network** for pixel-level land-cover classification.
- **NDVI and NDWI spectral analysis** for vegetation and water-body monitoring.
- **Temporal LSTM forecasting** for predictive environmental intelligence.

This multi-modal architecture combines visual understanding, spectral information, and temporal reasoning to improve both detection accuracy and environmental interpretation.

The custom U-Net segmentation model performs semantic segmentation on **256 × 256** satellite imagery, classifying every pixel into four land-cover categories:

- Mining
- Vegetation
- Water Bodies
- Normal Land

<div class="row justify-content-center mt-4">
  <div class="col-md-6">
    {% include figure.liquid
      path="assets/img/unet_prediction_sample.png"
      class="img-fluid rounded shadow"
    %}
  </div>
</div>

The segmentation network achieves **93% validation accuracy**, providing reliable localization of environmentally sensitive regions while improving downstream prediction performance.

---

#### AI-driven Enforcement Prioritization

Environmental agencies often receive far more suspected violations than can realistically be inspected.

SEVAS addresses this challenge through an intelligent prioritization framework that evaluates each detected case using multiple environmental and operational factors, including:

- Estimated environmental impact
- Severity of land degradation
- Legal confidence
- Prediction confidence
- Operational urgency

Each violation is assigned a priority score, allowing authorities to focus field inspections on the highest-risk locations while substantially reducing manual analysis effort.

---

#### Cross-Jurisdictional Intelligence

Illegal mining operations frequently extend beyond administrative boundaries.

SEVAS performs spatial and temporal correlation across districts and states to identify coordinated illegal activities, recurring operational patterns, and repeat offenders. This enables environmental agencies to uncover organized criminal networks and automatically route alerts to the appropriate jurisdiction.

---

#### Advanced Remote Sensing Analysis

SEVAS incorporates multiple remote sensing techniques commonly used in environmental monitoring.

These include:

- **NDVI (Normalized Difference Vegetation Index)** for vegetation health assessment.
- **NDWI (Normalized Difference Water Index)** for water-body extraction.
- Cloud detection and filtering to reduce false positives.
- Multi-temporal change detection for before-and-after environmental comparison.

By combining spectral information with deep learning predictions, the system achieves more robust environmental monitoring under varying weather and seasonal conditions.

---

#### Explainable Environmental Intelligence

Beyond identifying environmental violations, SEVAS generates interpretable outputs suitable for decision-makers.

For every detected case, the platform produces:

- Natural-language violation descriptions
- Confidence scores
- Severity assessment
- Estimated environmental impact
- Inspection recommendations

These explanations transform raw AI predictions into actionable intelligence that can directly support environmental enforcement and policy decisions.

---

#### Production-Ready Deployment

SEVAS is designed as a scalable environmental monitoring platform suitable for integration into government dashboards and enterprise systems.

The backend provides:

- RESTful API with **9+ endpoints**
- Real-time satellite image analysis
- Batch processing of multiple images
- Support for **JPG, PNG, TIFF, and GeoTIFF**
- Structured JSON responses
- CORS-enabled frontend integration
- Modular Flask-based deployment

This architecture enables automated environmental monitoring at regional or national scale while remaining flexible enough for research and operational deployments.

#### Machine Learning Pipeline

---
                        Input Image (Satellite/Drone)
                                    │
                                    ├──> Preprocessing
                                    │      ├─ Resize (256x256)
                                    │      ├─ Normalize (0-1)
                                    │      └─ Format validation
                                    │
                                    ├──> Spectral Analysis
                                    │      ├─ NDVI calculation
                                    │      ├─ NDWI calculation
                                    │      └─ Cloud detection
                                    │
                                    ├──> Vision AI Analysis
                                    │      ├─ Natural language description
                                    │      ├─ Violation detection
                                    │      └─ Confidence scoring
                                    │
                                    └──> U-Net Segmentation
                                        ├─ Pixel-level classification
                                        ├─ Mask generation
                                        └─ Area calculation
                                                │
                                                ▼
                                        Unified Results
                                        ├─ Violation: Yes/No
                                        ├─ Severity: Low/Medium/High
                                        ├─ Location: Description
                                        ├─ Area: Hectares
                                        ├─ Confidence: %
                                        └─ Recommendations
                                                

---

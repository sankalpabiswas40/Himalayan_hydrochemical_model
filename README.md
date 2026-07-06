# Himalayan_hydrochemical_model
# 🏔️ Himalayan HydroGeochem Predictor

**A 2D Spatial Prediction Model for Trace Element Kinetics in the Alaknanda-Ganga Basin**

![Live Demo](https://img.shields.io/badge/Live_Demo-Click_Here-blue?style=for-the-badge)

## 📖 Abstract
The Himalayan HydroGeochem Predictor is an interactive, browser-based spatial modeling tool designed to predict trace element concentrations (Fe, Mn, Cu, Pb, Zn, Cr, As, Cd, Ni) across the Alaknanda-Ganga river network and underlying groundwater aquifers. Built for hydrogeologists and environmental scientists, the tool uses a **Log-Additive Kinetic Model** that dynamically scales an Inverse Distance Weighting (IDW) baseline using four localized geochemical parameters: Lithological weathering, Hydraulic residence time, Clay sorption, and Redox potential.

This project was developed during the prestigious **IASc-INSA-NASI Summer Research Fellowship Programme (SRFP)** at **IISER Pune** to address spatial data scarcity in high-altitude Himalayan catchments.

---

## 🔬 Mathematical Methodology: The V3 Model

The core of the prediction engine relies on the V3 Log-Additive Model. For any given trace element $e$ at coordinates $(\phi, \lambda)$, the predicted concentration is defined as:

$$C_{predicted} = C_{IDW} \times \max\Big[0.1, \;\; (P_{lith} \cdot W_1) + P_{res} + P_{sorp} + P_{redox} \Big]$$

Where the multipliers represent:
1. **$C_{IDW}$ (Baseline Interpolation):** Derived from known field samples using Haversine distance-decay ($p=2$).
2. **$P_{lith}$ (Lithology Factor):** A matrix multiplier based on the underlying geology (e.g., Basalt releases 1.8x more Fe than standard Gneiss).
3. **$P_{res}$ (Residence Time):** Modeled as $e^{-\lambda \cdot v}$, where $v$ is surface water velocity derived from empirical discharge, driving dissolution rates.
4. **$P_{sorp}$ (Clay Sorption):** Modeled as $\log_{10}(10 + K_d/v)$, accounting for suspended sediment scavenging.
5. **$P_{redox}$ (Thermodynamics):** Arrhenius-style temperature dependency ($R_e \cdot e^{-0.05 \cdot T}$).

The interactive UI allows researchers to adjust the weights ($W_1 \ldots W_4$) in real-time to calibrate the model against localized conditions.

---

## ⚠️ Limitations & Uncertainties

As with any spatial model, transparency regarding uncertainties is critical:
1. **Data Sparsity:** The current baseline relies on highly localized hard-points (e.g., Chakrapani 2005) and synthetic datasets. True basin-wide accuracy requires dense, empirical sampling across the upper catchment. 
2. **Isotropic Assumption:** The IDW engine assumes isotropic dispersion. In reality, Himalayan fractured-rock aquifers exhibit highly anisotropic groundwater flow paths driven by complex fault systems (e.g., MCT, MBT).
3. **Chemical Speciation:** The model currently predicts total elemental concentrations. It does not dynamically partition between oxidation states (e.g., highly toxic As(III) vs less toxic As(V)), which are strongly pH/Eh dependent.

---

## 🚀 Future Scope

- **Machine Learning Integration:** Transitioning the static IDW baseline to a Random Forest or XGBoost model trained on comprehensive hydrochemical survey data.
- **Real-Time API Telemetry:** Integrating live data feeds from CWC (Central Water Commission) discharge gauges to dynamically update velocity and turbidity parameters.
- **3D Flow Modeling:** Connecting the 2D surface projection to a MODFLOW backend for true three-dimensional aquifer transport modeling.

---

## 🛠️ Tech Stack
- **Frontend:** HTML5, CSS3 (Glassmorphism UI), Vanilla JavaScript
- **Geospatial Engine:** Leaflet.js (CartoDB Positron tiles)
- **Spatial Topology:** Turf.js (Point-in-Polygon lithology resolution)
- **Data:** GeoJSON (River networks, Geological boundaries)

## 🤝 Acknowledgements
- **Project Developer:** Sankalpa Biswas (IASc-INSA-NASI SRFP Fellow).
- **Conceptualization & Mentorship:** Deepest gratitude to **Dr. Gyana Ranjan Tripathy** for providing the core idea and continuous guidance throughout this project.
- **Host Institution:** **IISER Pune** for hosting the fellowship and providing critical informational resources.
- **Data & Baseline Parameters:** Derived from Chakrapani (2005) and geological polygon mapping via the Bhukosh portal (GSI).
- **AI Assistance:** Advanced data extraction, scripting, and code architecture assisted by Google DeepMind Antigravity, Gemini, and Anthropic Claude.

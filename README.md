
# 🔥 Fire Spread Prediction using CNN + PINN

This project integrates **Convolutional Neural Networks (CNN)** and **Physics-Informed Neural Networks (PINN)** to predict wildfire spread rate by combining image-based feature extraction with physics-driven modeling.

Understand real-world fire behavior 
→ Identify data modalities (image, terrain, fire logs)
→ Choose CNN to perceive fire features
→ Choose PINN to embed fire dynamics
→ Combine both models
→ Validate with physics and data
→ Refine based on performance, realism, and explainability

## 📌 Objective

To accurately predict the **rate of fire spread (ROS)** using:
- Visual features extracted from labeled fire images (fuel type, texture, etc.)
- Elevation and slope from Digital Elevation Model (DEM)
- Geolocation (Latitude, Longitude) and time
- Advection-diffusion based PINN structure to incorporate physical laws of fire propagation

---

## 📂 Project Structure

- `Fire_CNN_PINN_Model_Final_v6.ipynb` – Refined version with model updates and RMSE-based evaluation
- `Fire_CNN_PINN_Model_Final.ipynb` – Original base implementation
- `/TIFF_input/` – DEM GeoTIFF files for terrain processing
- `PT-FireSprd_L2_FireBehavior_FULL_set.ods` – Portuguese wildfire dataset
- `/train_images/`, `/test_images/` – Wildfire image datasets labeled by fuel type

---

## 🔍 Methodology Overview

### 1. **CNN Module**
- Inputs: 128x128 wildfire images
- Outputs: 4 continuous features:
  - **Texture Smoothness**
  - **Vegetation Type** (scaled: GR = 0–1, GS = 1–2, SH = 2–3, TL = 3–4, NB = 4–5)
  - **Color Intensity**
  - **Terrain Complexity**
- Preprocessing: Resize, rotation, flipping augmentations
- Architecture: Custom CNN trained on labeled image sets

### 2. **PINN Module**
- Inputs: CNN features + slope + elevation + lat/lon + time
- Governing PDE: **Advection-Diffusion Equation** for fire spread
- Loss Function:
  - Supervised MSE loss on ROS targets
  - Physics-informed residual loss
  - Total Loss = Data Loss + λ * Physics Loss
- Output: Predicted **Rate of Spread (ROS)** in m/h

---

## 📈 Evaluation Metrics

- **RMSE (Root Mean Squared Error)** used for performance
- Ideal RMSE should be as low as possible (context-dependent, ~10–30 m/h reasonable)
- RMSE has **units of ROS** (meters/hour), since it's derived from differences in predicted vs actual ROS

---

## 🧪 Data Processing

- DEM files processed to extract **elevation** and compute **slope** using gradient methods
- Portuguese dataset parsed to align image inputs with ROS targets
- CNN predictions fed into PINN training dynamically

---

## ✅ Strengths

- Combines **data-driven learning** with **physics-based reasoning**
- Handles real terrain and fire spread variability
- Robust to small datasets due to physical constraints

---

## ⚠️ Challenges

- Requires labeled wildfire images with accurate GPS tags
- High computation due to dual training of CNN and PINN
- Elevation/slope interpolation needs fine-grained georeferencing

---

## 🚀 Future Improvements

- Integrate **weather conditions** (wind, humidity, temperature)
- Train CNN using **transfer learning** on satellite imagery
- Add **temporal sequence modeling** with RNN or Transformers
- Incorporate **fuel moisture content** and dynamic vegetation updates
- Validate using **real wildfire incidents** from multiple countries


# Dynamic Pricing Lots - Real-Time Data Processing

> **Capstone Project - Summer Analytics 2025**  
> Author: **Dhairya Pandya**  
> Repository: `Dynamic Pricing Lots - Real-Time Data Processing`

---

## 🚀 Objective

To build a real-time intelligent pricing engine for 14 urban parking lots that:
- Adjusts prices dynamically based on demand, traffic, and other features
- Processes data as live streams using **Pathway**
- Visualizes pricing trends in real time using **Bokeh**
- Implements multiple models with increasing sophistication

---

## 🧠 Models Implemented

### 🔹 Model 1 – Baseline Linear Model

> A simple model based on real-time occupancy levels.

**Formula (Readable):**  
`Price_t = BasePrice + α × min(Occupancy / Capacity, 1)`

**Rendered Formula:**  
![Model 1](https://latex.codecogs.com/png.image?%5Cdpi%7B150%7D%20Price_t%3DBasePrice%2B%5Calpha%5Ccdot%20%5Cmin%5Cleft(%5Cfrac%7BOccupancy%7D%7BCapacity%7D%2C1%5Cright))

- Base price: $10  
- α (alpha): scaling constant (e.g. 5)  
- Clipped to: $[10, 15]  
- Updates every stream step using Pathway.

---

### 🔹 Model 2 – Demand-Based Pricing (Advanced)

> Considers multiple real-world features influencing demand.

**Demand Function (Readable):**  
`D = α × (Occupancy / Capacity) + β × QueueLength - γ × TrafficLevel + δ × SpecialDay + ε × VehicleTypeWeight`

**Rendered Formula:**  
![Demand Function](https://latex.codecogs.com/png.image?%5Cdpi%7B150%7D%20D%20%3D%20%5Calpha%20%5Ccdot%20%5Cleft(%5Cfrac%7BOccupancy%7D%7BCapacity%7D%5Cright)%20%2B%20%5Cbeta%20%5Ccdot%20QueueLength%20-%20%5Cgamma%20%5Ccdot%20TrafficLevel%20%2B%20%5Cdelta%20%5Ccdot%20SpecialDay%20%2B%20%5Cepsilon%20%5Ccdot%20VehicleTypeWeight)

**Pricing Rule (Readable):**  
`Price_t = BasePrice × (1 + λ × NormalizedDemand)`

**Rendered Formula:**  
![Pricing Rule](https://latex.codecogs.com/png.image?%5Cdpi%7B150%7D%20Price_t%3DBasePrice%20%5Ccdot%20%281%20%2B%20%5Clambda%20%5Ccdot%20NormalizedDemand%29)

---

### 🔹 Model 3 – Competitive Pricing Model (Optional)

> Introduces **location awareness** and **rerouting logic**.

**Conceptual Rule:**  
`Price_t = f(OwnDemand, CompetitorPrices, Proximity)`

---

## 📦 Dataset Info

- 14 parking lots × 73 days × 18 time steps/day
- Features:
  - `Occupancy`, `Capacity`, `QueueLength`
  - `TrafficConditionNearby`, `IsSpecialDay`
  - `VehicleType` (car, bike, truck)
  - `Latitude`, `Longitude` (for competition modeling)

---

## 🧱 System Architecture (Mermaid)

```mermaid
flowchart TD
    A[Raw CSV Input] --> B[Preprocessing & Feature Engineering]
    B --> C[Model 1: Baseline Pricing]
    B --> D[Model 2: Demand-Based Pricing]
    B --> E[Model 3: Competitive Pricing]
    C --> G[Price Stream Table]
    D --> G
    E --> G
    G --> H[Pathway Windowed Aggregation]
    H --> I[Bokeh Real-Time Visualization]
```

---

## 🛠️ Technologies Used

- **📊 Bokeh** – interactive time-series plots
- **⚡ Pathway** – for real-time stream simulation
- **🧮 Numpy & Pandas** – all models implemented from scratch
- **📁 Google Colab** – runtime environment

---

## 📈 Visualization Strategy

- **Real-time line plots** for each parking space
- Snapshots generated using `head()` after `pw.run()`
- Plotted with custom function `plot_snapshot(...)`
- Supports comparison across all lots or specific ones

---

## ✅ Output Example

| Time              | SystemCodeNumber | Price ($) |
|-------------------|------------------|-----------|
| 2025-07-01 08:00  | BHMBCCMKT01      | 12.50     |
| 2025-07-01 08:30  | BHMBCCMKT01      | 13.10     |

---

## 📍 How to Run

```python
# After executing all model logic
pw.run()

```

---

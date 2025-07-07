# 📄 Dynamic Pricing for Urban Parking Lots - Final Report

**Capstone Project | Summer Analytics 2025**  
**Consulting & Analytics Club × Pathway**

---

## 1. 📆 Introduction

Urban parking lots experience demand fluctuations throughout the day. Static pricing does not account for real-time factors like traffic, queue length, or nearby competition, leading to inefficiencies.

This report outlines the development of a **real-time dynamic pricing system** that adjusts parking prices based on historical and real-time factors.

---

## 2. 🔬 Dataset Overview

- **Locations:** 14 urban parking lots
- **Duration:** 73 days
- **Sampling:** 18 time points/day (8:00 AM - 4:30 PM)
- **Features:**
  - Latitude & Longitude
  - Capacity & Occupancy
  - Queue Length
  - Incoming Vehicle Type (Car/Bike/Truck)
  - Nearby Traffic Level
  - Special Day Indicator

---

## 3. 💡 Pricing Models

### 3.1 Baseline Linear Model
- **Logic:** Price increases linearly with occupancy.
- **Formula:**
  ```
  Price(t+1) = Price(t) + α * (Occupancy / Capacity)
  ```
- **Purpose:** Serve as a simple baseline.

### 3.2 Demand-Based Pricing Model
- **Features Used:**
  - Occupancy / Capacity
  - Queue Length
  - Traffic Level
  - Special Day (binary)
  - Vehicle Type (weighted)

- **Demand Function:**
  ```
  Demand = α * (Occupancy / Capacity) + β * QueueLength - γ * Traffic + δ * SpecialDay + ε * VehicleType
  ```

- **Price Calculation:**
  ```
  Price = BasePrice * (1 + λ * NormalizedDemand)
  ```

- **Constraints:**
  - Price bounded between 0.5x and 2x of Base Price.
  - Smooth price transitions.

### 3.3 Competitive Pricing Model
- **Additional Factors:**
  - Geographical proximity of nearby lots.
  - Competitor prices.

- **Logic:**
  - If nearby lots are cheaper → lower price or suggest rerouting.
  - If nearby lots are expensive → increase price while staying competitive.

---

## 4. 🔧 Performance Issue with Competitive Pricing Model

### Problem:
The competitive pricing model suffers from slow performance due to nested loops performing expensive distance calculations for each lot pair. This results in O(N²) complexity.

### Optimized Solutions:
- **Spatial Indexing (KDTree):** Improve distance lookup time to O(log N).
- **Parallel Processing:** Use multiprocessing to split the workload.
- **Distance Matrix:** Calculate distances once using `scipy.spatial.distance.cdist` and reuse them.
- **Sampling Strategy:** Run competitive pricing on small data samples for faster iterations.

### Recommended Approach:
1. **Phase 1:** Quick fix - skip competitive pricing temporarily.
2. **Phase 2:** Implement distance matrix and sampling(Requires scikit-learn for Optimized Output).
3. **Phase 3 (Advanced):** Add KDTree and parallelization for production-level performance(Requires scikit-learn).

---

## 5. 📊 Feature Engineering

- **Normalized Occupancy:** Occupancy / Capacity.
- **Traffic Levels:** Standardized across time periods.
- **Vehicle Type Weights:** Assigned based on parking space usage.
- **Demand Normalization:** Applied Min-Max normalization to keep demand in a bounded range.

---

## 6. 📊 Results Summary

- Baseline Model showed a basic upward trend with occupancy.
- Demand-Based Model showed more reactive and contextual pricing.
- Competitive Pricing allowed for smart adjustments based on nearby lots, once optimized.

**Visualization:** Real-time price curves and competitor comparisons were generated using Bokeh.

---

## 7. 🔍 Assumptions

- Base price = $10 for all lots.
- Maximum price variation capped at 2x Base Price.
- Nearby lot distance threshold of ~500 meters for competitive analysis.
- Traffic & Special Day impacts are linear and additive in the demand function.

---

## 8. 🔬 Limitations & Future Work

### Limitations
- Simple linear demand formulation.
- No user-level behavioral modeling.
- Static feature weights without optimization.

### Future Improvements
- Learn optimal feature weights using historical data.
- Add surge pricing for peak periods.
- Integrate rerouting recommendations in the dashboard.
- Build automated model retraining pipelines.

---

## 9. 🙏 Acknowledgements

- **Consulting & Analytics Club, IIT Patna**
- **Pathway.ai** for the real-time streaming engine.

---

## 10. 🌟 Key Takeaways

- Real-time pricing creates a more efficient parking lot ecosystem.
- Pathway enables seamless data streaming and feature processing.
- Visualizing dynamic pricing provides transparency and explainability to stakeholders.

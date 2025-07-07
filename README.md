# 🚗 Dynamic Pricing for Urban Parking Lots

Capstone Project for **Summer Analytics 2025**  
Organized by the **Consulting & Analytics Club × Pathway**

---

## 📖 Problem Statement

Urban parking lots face fluctuating demand, but static pricing fails to optimize space utilization.  
This project builds a **real-time dynamic pricing engine** that adjusts parking prices based on:

- Lot occupancy
- Queue lengths
- Traffic congestion
- Special events
- Competitor prices
- Vehicle type

---

## 🛠️ Tech Stack

| Layer              | Tools & Libraries                                         |
|--------------------|-----------------------------------------------------------|
| Programming        | Python 3.x                                                |
| Data Processing    | NumPy, Pandas                                             |
| Real-time Pipeline | Pathway                                                   |
| Visualization      | Bokeh                                                     |
| Environment        | Google Colab                                              |
| Version Control    | Git, GitHub                                               |

---

## 🔨 Architecture Flow

### ⛳ **Overall Workflow:**

1. **Data Simulation:**
   - Real-time parking data streamed through **Pathway**.
   - Time-stamped events: occupancy, queue, traffic, special days, etc.

2. **Real-Time Data Ingestion:**
   - Pathway dynamically ingests incoming data in chronological order.

3. **Pricing Engine:**
   - **Model 1:** Baseline linear pricing based on occupancy.
   - **Model 2:** Demand-based pricing using multiple features.
   - **Model 3:** Competitive pricing based on nearby lot prices and geospatial data.

4. **Real-Time Visualization:**
   - Prices visualized in real-time via Bokeh dashboards.

---

### 🏠 **Architecture Diagram**

                             +--------------------------+
                             |   Parking Lot Dataset    |
                             +--------------------------+
                                       |
                                       V
                             +--------------------------+
                             | Real-Time Data Simulator |
                             |  (Pathway Streams)      |
                             +--------------------------+
                                       |
                                       V
                             +--------------------------+
                             |    Dynamic Pricing      |
                             |        Engine           |
                             +--------------------------+
                                |          |         |
                                V          V         V
                    +--------------+ +--------------+ +--------------+
                    |  Baseline    | | Demand-based| | Competitive   |
                    |   Linear     | |   Model     | | Pricing Model |
                    +--------------+ +--------------+ +--------------+
                                       |
                                       V
                             +--------------------------+
                             | Real-time Pricing Output |
                             +--------------------------+
                                       |
                                       V
                             +--------------------------+
                             |   Bokeh Visualization    |
                             +--------------------------+

---

## 🧠 Model Details

### Model 1: Baseline Linear Model
> Price ∝ Occupancy / Capacity  
Simple linear relationship:  
```
Price(t+1) = Price(t) + α * (Occupancy / Capacity)
```

### Model 2: Demand-Based Model
Multivariate demand function based on:
- Occupancy rate
- Queue length
- Traffic congestion
- Special events
- Vehicle type

Example:
```
Demand = α * (Occupancy / Capacity) + β * QueueLength - γ * Traffic + δ * SpecialDay + ε * VehicleType
Price = BasePrice * (1 + λ * NormalizedDemand)
```

### Model 3: Competitive Pricing Model (Advanced)
- Adjust prices based on competitor parking lots using distance and price difference.
- If nearby lots are cheaper and available → decrease price.
- If nearby lots are expensive → increase price.

---

## 🚀 Setup & Run

### Prerequisites
- Python 3.x
- Google Colab
- Libraries: `pandas`, `numpy`, `bokeh`, `pathway`

### Installation
```bash
pip install pandas numpy bokeh pathway
```

### Run in Google Colab
1. Upload the `Dynamic_Pricing_Model.ipynb` notebook.
2. Execute each cell in order.
3. Launch Bokeh visualization on Colab.
4. Access the interactive dashboard.

---

## 📊 Visualization Output

- Real-time price curves for each lot.
- Competitor price comparisons.
- Smooth price transitions visible across time.

---

## 📂 Project Structure
```
.
├── Dynamic_Pricing_Model.ipynb    # Main implementation notebook
├── capstone_dataset.csv           # Raw dataset
├── problem statement.pdf          # Problem description
└── README.md                      # This file
```
---

## 🙏 Acknowledgements

- **Consulting & Analytics Club, IIT Patna**
- **Pathway.ai** for the real-time data processing framework.

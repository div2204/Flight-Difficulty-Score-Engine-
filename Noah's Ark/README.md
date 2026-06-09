# UA SkyHack 3.0: Data-Driven Flight Difficulty Score

## 1. Project Overview

### Problem
Frontline teams at major hubs like Chicago O'Hare (ORD) must manage hundreds of daily departures. However, not all flights are equally complex. Currently, identifying high-difficulty flights relies on experience, an approach that is inconsistent, reactive, and difficult to scale. This leads to missed opportunities for proactive resource allocation and can contribute to network delays.

### Solution
This project develops a **data-driven Flight Difficulty Score** that systematically quantifies the operational complexity of each flight. By analyzing passenger, baggage, and service data, our model provides a daily ranking and classification system. This enables ground teams to move from a reactive to a proactive operational posture, anticipating challenges and allocating resources with precision to mitigate delays.

---

## 2. Methodology: From Data to Decision

Our approach transforms raw operational data into a simple, actionable score through a multi-step pipeline executed in a Jupyter Notebook.

### Step 1: Data Aggregation & Preparation
- Consolidated five disparate datasets into a single, comprehensive view.  
- Aggregated all passenger, baggage, and Special Service Request (SSR) data to a unique flight-and-day level.  
- Standardized date/time fields and computed key metrics such as departure delay.

### Step 2: Feature Engineering
Engineered features to capture true operational complexity:

- **pax_load_ratio**: Total Passengers / Total Seats  
- **ground_constraint**: Binary flag for flights with minimal turnaround time  
- **bag_load_ratio**: Total Bags / Total Seats  
- **transfer_ratio**: Transfer Bags / Checked Bags  

### Step 3: Daily Normalization (Scaling)
Normalized all features daily using `scikit-learn`’s `MinMaxScaler` to convert each feature into a 0–1 score relative to other flights on the same day.

### Step 4: Scoring, Ranking & Classification
- **Score Formula**: `(Average of Normalized Features) * 100`  
- **Ranking**: Flights ranked daily (Rank 1 = most difficult).  
- **Classification**: Quantile-based segmentation (`pandas.qcut` + `numpy.select`) into three tiers — *Difficult*, *Medium*, *Easy*.

---

## 3. How to Run the Code

All analysis is contained within a single Jupyter Notebook: **`d.ipynb`**

### Prerequisites
- Python 3.x  
- Jupyter Notebook (or VS Code with Jupyter extension)  
- Required libraries:
  ```bash
  pip install pandas numpy scikit-learn matplotlib seaborn
  ```

### Execution Steps
1. **Unzip the Files** – Place all project files in one directory (notebook + source CSVs).  
2. **Open the Notebook** – Launch Jupyter and open `d.ipynb`.  
3. **Run the Analysis** –  
   - Run all cells: *Kernel → Restart & Run All*, or  
   - Run sequentially: *Shift + Enter*

### Output
After running, a file named **`difficulty_score.csv`** will be created containing:
- Difficulty score (0–100 scale)  
- Daily rank  
- Classification (*Difficult*, *Medium*, *Easy*)

---

## 4. Context

This analysis was developed for the **United Airlines SkyHack 3.0** challenge, demonstrating how data-driven approaches can improve flight operations and ground efficiency.

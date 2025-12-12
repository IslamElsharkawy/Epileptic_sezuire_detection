## 🔬 Epileptic Seizure Recognition Project Overview

This project uses Machine Learning to analyze brain activity signals (Electroencephalogram - EEG) and automatically detect whether a recording contains an epileptic seizure.

### 🎯 The Main Goal

The primary objective is to transform raw EEG signals into meaningful statistical features and use them to train a model that can reliably classify a 1-second EEG segment as either **Seizure (1)** or **No Seizure (0)**.

### 📂 Data Source

* **Dataset:** Epileptic Seizure Recognition (from Kaggle).
* **Link:** **[https://www.kaggle.com/datasets/harunshimanto/epileptic-seizure-recognition](https://www.kaggle.com/datasets/harunshimanto/epileptic-seizure-recognition)**
* **Data Type:** Time series data representing electrical activity of the brain.
* **Input:** Each row is a 1-second slice of brain activity, represented by 178 time points.
* **Target:** The original 5-class problem was simplified into a **Binary Classification** task.

---

### 🛠️ Key Techniques Used

The project relies on a critical two-step process:

#### 1. Feature Engineering (Signal Processing)

Raw time-series data was converted into numerical features that capture its energy and shape, making it suitable for ML models.

| Feature Type | Technique | Purpose/What It Measures |
| :--- | :--- | :--- |
| **Frequency Domain** | **Welch's Method (PSD)** | Measures how the signal's energy is distributed across different brain frequencies (e.g., Delta, Alpha, Beta, Gamma).  |
| **Time Domain** | **Statistical Moments** | Measures the shape and variability of the wave, including **Standard Deviation (STD)** for signal amplitude, **Skewness** for asymmetry, and **Kurtosis** for the sharpness of the signal's peaks (important for detecting abnormal 'spikes'). |

#### 2. Machine Learning Models

Three models were trained and compared after robust data splitting (`GroupShuffleSplit` was used to ensure data from the same patient was not mixed between the training and test sets).

| Model | Role | Accuracy | AUC (Discrimination) | Recall (Seizure) |
| :--- | :--- | :--- | :--- | :--- |
| **Decision Tree (DT)** | Non-linear classifier | **0.9669** | 0.9616 | **0.92** |
| **Logistic Regression (LR)** | Linear classifier | 0.9643 | 0.9849 | 0.91 |
| **SVM** | Complex classifier | 0.9630 | **0.9916** | 0.91 |

### ✅ Conclusion

The **Decision Tree** model was selected as the best choice for clinical application. Its superior **Recall (0.92)** for the Seizure class is crucial, as the priority in medical diagnosis is to minimize **False Negatives** (missed seizures).

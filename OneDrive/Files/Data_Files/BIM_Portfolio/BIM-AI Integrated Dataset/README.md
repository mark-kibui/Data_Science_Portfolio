# **BIM & AI Civil Engineering Dataset Analysis**

## **1. Dataset Overview**

This dataset facilitates whole life cycle management of civil engineering projects by integrating **Building Information Modeling (BIM)** and **Artificial Intelligence (AI)**. It encompasses key project data such as **cost, schedule, structural health, environmental conditions, resource allocation, safety risks, and drone-based monitoring**.

### **Key Features**

- **Project Metadata:** Project type (bridge, road, building, etc.), location, timeline
- **Financial Data:** Planned vs. actual cost, cost overruns
- **Scheduling Data:** Planned vs. actual duration, schedule deviation
- **Structural Health Monitoring:** Vibration levels, crack width, load-bearing capacity
- **Environmental Factors:** Temperature, humidity, air quality, weather conditions
- **Resource & Safety Management:** Material usage, labor hours, equipment utilization, accident records
- **Drone-Based Monitoring:** Image analysis scores, anomaly detection, completion percentage
- **Target Variable:** **Risk Level** (Low, Medium, High) based on cost, schedule, safety, and structural health

---

## **2. Data Quality Checks**

### **Missing Values**
- Checked for missing values and handled appropriately.

### **Duplicate Rows**
- Removed duplicate records to maintain data integrity.

### **Unique Values in Categorical Features**
<style>
    table {float: left; margin-right: 20px;}
</style>

| Feature            | Unique Values                               |
| :---------------- | :------------------------------------------ |
| **Project_Type**  | Bridge, Road, Building                     |
| **Location**      | New York, Los Angeles, Chicago, Houston    |
| **Weather_Condition** | Sunny, Rainy, Snowy, Stormy            |
| **Risk_Level**    | Low, Medium, High                          |

---

## **3. Anomaly Detection**

### **Negative or Unrealistic Values**

| Feature              | Count of Negative Values |
| :------------------- | :----------------------- |
| **Cost_Overrun**     | 164                       |
| **Schedule_Deviation** | 170                     |
| **Temperature**      | 170                       |

#### **Interpretation**
- **Cost Overrun** should not be negative. Negative values indicate cost savings instead of overruns.
- **Schedule Deviation** can be negative, meaning some projects finished earlier than planned.
- **Temperature** should not be negative unless projects are in extremely cold regions.

#### **Next Actions**
- Convert **Cost Overrun** to absolute values or redefine as **Cost Savings**.
- Keep **Schedule Deviation** but consider an additional **Project Efficiency Score**.
- Investigate **negative temperatures** and replace errors with median values.

---

### **Outliers Detection (IQR Method)**
- Detected extreme values in numerical features.

#### **Next Actions**
- Visualize **Cost Overrun** and **Schedule Deviation** distributions.
- Consider **transformation or capping** extreme values if necessary.

---

## **4. Skewness & Kurtosis Analysis**

### **Skewness (Data Symmetry)**
| Feature              | Skewness |
| :------------------- | :------- |
| **Cost_Overrun**     | 0.93     |
| **Schedule_Deviation** | 0.77   |

#### **Interpretation**
- **Cost Overrun and Schedule Deviation** are **right-skewed**, meaning some projects have extremely high values.
- Possible action: **Log transformation** to normalize the distribution.

---

### **Kurtosis (Extreme Values & Tails)**
| Feature              | Kurtosis |
| :------------------- | :------- |
| **Cost_Overrun**     | 0.11     |
| **Schedule_Deviation** | -0.02  |

#### **Interpretation**
- Values have **negative kurtosis**, meaning fewer extreme outliers.
- No immediate need for outlier removal, but further analysis on **high-risk projects** is recommended.

---

## **5. Model Selection & Performance Evaluation**

### **Baseline Model: Logistic Regression**
| Metric           | Score  |
| :-------------- | :----- |
| **Accuracy**    | 97.5%  |
| **Precision (avg)** | 98%  |
| **Recall (avg)** | 97%  |
| **F1-score (avg)** | 98%  |

#### **Confusion Matrix Breakdown**
- **Low Risk:** Precision **91%**, Recall **100%**, F1-score **95%**
- **Medium Risk:** Precision **98%**, Recall **94%**, F1-score **96%**
- **High Risk:** Precision **99%**, Recall **99%**, F1-score **99%**

### **Alternative Model: Random Forest**
| Metric           | Score  |
| :-------------- | :----- |
| **Accuracy**    | 93.5%  |
| **Precision (avg)** | 94%  |
| **Recall (avg)** | 94%  |
| **F1-score (avg)** | 94%  |

#### **Key Observations**
- **Logistic Regression** outperformed **Random Forest** in terms of overall accuracy and precision.
- **Random Forest** struggled slightly with classifying **High Risk** projects accurately.
- Given the dataset size (1000 rows), **high performance is expected** due to well-defined patterns.

### **Final Model Selection: Logistic Regression**
- **Chosen due to higher accuracy and stability** across all risk levels.
- Model is simple, interpretable, and effective for risk classification.

---

## **6. Next Steps**
- **Deploy the Logistic Regression model** for risk classification.
- **Create a dashboard** for risk analysis and prediction visualization.
- **Explore real-time monitoring** by integrating with **BIM software** for automated risk assessment.

---

## **7. Conclusion**
This project successfully built a **Risk Prediction Model for Civil Engineering Projects** using **BIM and AI-driven analysis**. By detecting anomalies, analyzing patterns, and training models, we achieved a **highly accurate risk assessment system** that can aid in **proactive decision-making** for construction projects.

**Next phase:** Deployment and integration with project management systems.

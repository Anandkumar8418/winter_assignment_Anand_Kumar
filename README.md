# Merchant and Transaction Data Generation Framework

This project provides tools for generating synthetic merchant profiles and transaction data with embedded fraudulent patterns. It includes feature engineering for analytics and model development for fraud detection.

---

## **Data Generation**

### **1. Merchant Profile Generator**
- Creates merchant profiles with both basic and additional fields.

### **2. Transaction Generator**
- Generates both normal and fraudulent transaction patterns.

---

## **Key Characteristics of the Generated Data**

### **Merchant Profiles**
- **Unique merchant IDs**: Each merchant is assigned a unique identifier.
- **Business Types**: Merchants belong to different business categories (e.g., Retail, E-commerce).
- **Registration Dates**: Randomly assigned registration dates within a given range.
- **GST Statuses**: Merchants have different GST statuses (Active, Inactive, Pending).
- **Fraudulent Flag**: 20% of the merchants are marked as fraudulent.
=======

---

### **Normal Transactions**
- **Volume**: Generates 50–200 transactions per merchant.
- **Dates**: Transaction dates are random within a specified period.
- **Amounts**: Follow a normal distribution (mean: 1000, std dev: 300).
- **Customer IDs**: Randomly assigned to each transaction.

---

### **Fraudulent Patterns**

#### **a. Late Night Pattern**
- **Volume**: Generates 20–50 transactions during unusual hours (11 PM–4 AM).
- **Amounts**: Higher average transaction amount (mean: 2000, std dev: 500).

#### **b. High Velocity Pattern**
- **Spike Day**: Picks a single "spike day" and generates 100–200 transactions.
- **Distribution**: Spreads transactions across the 24 hours.
- **Amounts**: Higher average transaction amount (mean: 1500, std dev: 400).

#### **c. Customer Concentration Pattern**
- **Dominance**: Assigns 80% of transactions to a single customer ID.
- **Volume**: Generates 50–150 transactions.
- **Amounts**: Normally distributed (mean: 1200, std dev: 300).

---
### **Example Data**
An example image of the generated data structure:
![Could Not Load Image](media/image.png)

--- 

## **Feature Engineering**

### **Function: `calculate_merchant_features`**

Generates a feature set for each merchant based on their transactions. Aggregates transaction data to compute metrics such as transaction velocity, amount distribution, time-based patterns, and customer concentration.

### **Output**
The function produces a DataFrame where each row represents a merchant, with aggregated features derived from their transaction data:

| **Feature Name**         | **Description**                                                                 |
|---------------------------|---------------------------------------------------------------------------------|
| `merchant_id`             | Unique identifier for the merchant.                                            |
| `avg_daily_txns`          | Average number of transactions per day for the merchant.                       |
| `max_daily_txns`          | Maximum transactions in a single day.                                          |
| `min_daily_txns`          | Minimum transactions in a single day.                                          |
| `std_daily_txns`          | Standard deviation of daily transaction counts.                                |
| `night_txn_ratio`         | Proportion of transactions occurring during night hours (10 PM–4 AM).          |
| `avg_amount`              | Average transaction amount.                                                    |
| `std_amount`              | Standard deviation of transaction amounts.                                     |
| `min_amount`              | Minimum transaction amount.                                                    |
| `max_amount`              | Maximum transaction amount.                                                    |
| `customer_concentration`  | Proportion of transactions from the most frequent customer relative to the total.|

---

### **How It Works**
1. **Transaction Velocity Metrics**:
   - Computes the average, maximum, minimum, and standard deviation of daily transaction counts.

2. **Time-Based Patterns**:
   - Analyzes the hourly distribution of transactions.
   - Calculates the proportion of transactions occurring during night hours (10 PM–4 AM).

3. **Amount Distributions**:
   - Extracts statistics such as mean, standard deviation, minimum, and maximum for transaction amounts.

4. **Customer Concentration**:
   - Determines the dominance of a single customer by calculating the proportion of transactions from the most frequent customer.

---

## **Model Development**

### **FraudDetectionAutoencoder**
- Implements an autoencoder with the following characteristics:
  - 3-layer encoder and decoder architecture.
  - Reconstruction error based on Mean Squared Error (MSE).
  - Automatic threshold calculation for anomaly detection.

---

## **Fraud Pattern Detection**

### **FraudPatternDetector**
Implements detection rules for identifying specific fraud patterns:
1. **High Velocity Spikes**: Detects sudden bursts of transaction volume within a short period.
2. **Odd-Hour Patterns**: Identifies transactions occurring during unusual hours.
3. **Customer Concentration**: Flags merchants with an unusually high percentage of transactions from a single customer.

---


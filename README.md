# 🍕 Slices & Stats: Predictive Delivery & Refund Optimization

This project addresses a critical business challenge for a pizza delivery store: the "30-Minute Guarantee." By leveraging Databricks and the Medallion Architecture, I built a system that predicts delivery delays before they happen, allowing the business to manage financial loss from free pizzas and improve customer satisfaction.

## 🏗️ Data Architecture (Medallion Layers)

The solution utilizes a three-tier architecture to ensure data quality and reliability:

Bronze (Raw Layer): Ingests raw synthetic order data including timestamps, distance, traffic levels, and kitchen prep times.

Silver (Cleaned/Enriched Layer): Applies business logic to calculate travel time and identifies orders eligible for a refund (is_late_refund). It also performs feature engineering for AI, extracting hour and day patterns.

Gold (Business Layer): Aggregates data to provide high-level insights into refund rates and average delivery times across different pizza types and traffic conditions.


## 🤖 AI Innovation & ML Component

To move from reactive reporting to proactive management, I implemented a Machine Learning workflow using MLflow:

Problem Framing: Predicting the probability of a delivery exceeding 30 minutes based on real-time factors like prep time, distance, and time of day.

Model Selection: Utilized a Random Forest Classifier to handle complex interactions between traffic and kitchen workloads.

Technical Reasoning: The model is tracked via MLflow to log accuracy metrics and version the model artifacts for easy deployment as a Spark UDF (User Defined Function).


## 📊 Business Impact & Insights

The Gold Analysis revealed that:

Traffic Sensitivity: Specific traffic levels are the primary driver for "Free Pizza" refunds.

Product Risk: Certain pizza types (e.g., BBQ Chicken) may have higher prep times, putting them in the "Danger Zone" for delays.

Proactive Alerts: By applying the ML model to orders in progress, the store can identify "at-risk" deliveries and notify customers proactively, transforming a potential complaint into a positive brand touchpoint.


## 🛠️ Technical Setup & Requirements

Platform: Databricks (Free Tier).

Governance: Unity Catalog (Catalog: pizza_factory).

Storage: Delta Lake with ACID transactions for data consistency.

Orchestration: Databricks Jobs (simulated via notebook workflow).

## How to Run

Catalog Setup: Execute the first SQL cell to initialize the pizza_factory catalog and schemas.

Data Pipeline: Run the Bronze and Silver cells to generate and transform the data.

Analytics: Execute the Gold SQL queries to generate the performance table.

Machine Learning: Run the MLflow cells to train the model and generate real-time predictions.

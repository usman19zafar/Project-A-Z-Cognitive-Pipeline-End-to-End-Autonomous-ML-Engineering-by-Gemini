🏆 Cognitive Pipeline Tournament: 

AI Decision SystemProject Overview

This project is an end-to-end Machine Learning and Deep Learning pipeline designed to predict consumer behavior. 
It automates the transition from raw, "dirty" data to a deployed, high-accuracy prediction engine. 
By staging a "tournament" between classical algorithms and modern neural networks, the system identifies the most efficient model for the specific dataset provided.

1. System ArchitectureThe project follows a modular design to ensure scalability and maintainability:
2. core/: Contains the Autonomous Preprocessor, the "brain" of the data cleaning phase.
3. engines/: Houses the Classifier Arena (Classical ML) and the DeepBrain (TensorFlow ANN).
4. data/: Managed storage for raw datasets and processed information.
5. models/: Persistent storage for serialized model binaries (.pkl files) and data scalers.

2. Technical Deep Dive

Data Engineering Pipeline
To prepare the 5,000-row dataset for the AI, the following transformations are applied:

Mean Imputation: Statistical recovery of missing values in numerical features.
One-Hot Encoding: Conversion of categorical variables (e.g., Country names) into binary vectors.
Label Encoding: Normalizing the target variable (Yes/No) into binary (1/0) for Deep Learning compatibility.
Feature Scaling: Application of StandardScaler to ensure features like "Age" and "Salary" contribute equally to the model's weight updates.

3. The Tournament Results
  
The system evaluated 7 models on a 20% hold-out test set.
```code
+----------------------+----------+----------+--------------+
|        Model         | Accuracy | F1-Score | Latency (ms) |
+----------------------+----------+----------+--------------+
| Random Forest        |  0.997   |  0.9970  |    373.32    |
| Kernel SVM (RBF)     |  0.996   |  0.9960  |    798.96    |
| Decision Tree        |  0.993   |  0.9930  |      6.23    |
| ANN (Neural Network) |  0.992   |  0.9920  |  23883.41    |
| Logistic Regression  |  0.949   |  0.9489  |     18.84    |
+----------------------+----------+----------+--------------+
```
```code
Key Findings
Tree-Based Superiority: Random Forest achieved near-perfect accuracy, proving its dominance in handling non-linear tabular data.

The Cost of Complexity: The ANN provided high accuracy but at a latency cost 60x higher than the Random Forest, suggesting that for this scale, classical ML is superior.

Linearity Gap: The drop in performance for Logistic Regression confirmed the decision boundary in the data is highly non-linear.
```

4. Deployment & Live Inference
  
The winning Random Forest model was serialized using joblib. 

A custom Inference Engine (predictor.py) was developed to:
1, Load the champion model and the specific data scaler used during training.
2, Accept real-time user input (Age/Salary).
3, Output a prediction with a calculated Confidence Interval.

5. How to Run
   
Install Requirements: pip install pandas scikit-learn tensorflow joblib pyyaml

Train & Evaluate: python main.py
Deploy Model: python deploy.py
Live Prediction: python predictor.py

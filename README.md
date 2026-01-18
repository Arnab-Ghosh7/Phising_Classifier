# Phishing Classifier

![Python](https://img.shields.io/badge/Python-3.7%2B-blue?style=for-the-badge&logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-2.0%2B-green?style=for-the-badge&logo=flask&logoColor=white)
![Scikit-Learn](https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)
![XGBoost](https://img.shields.io/badge/XGBoost-EB3429?style=for-the-badge&logo=xgboost&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-07405E?style=for-the-badge&logo=sqlite&logoColor=white)

## 📖 Overview

In today's digital landscape, phishing attacks remain one of the most prevalent security threats. This **Phishing Classifier** is a sophisticated Machine Learning web application engineered to detect and classify phishing websites with high accuracy. By analyzing over 30 distinct URL-based features—such as IP address presence, URL length, SSL state, and domain registration length—the system can identify malicious intent hidden within web addresses.

The application is built upon a modular and scalable architecture that separates data ingestion, validation, preprocessing, and model training into distinct components. This ensures valid training data through rigorous schema checks and enhances prediction reliability. Under the hood, it employs a **Clustering-Verification-Ensemble** approach: data is first clustered using K-Means to identify underlying patterns, and then a dedicated XGBoost model is trained for each cluster. This granular approach allows the system to handle diverse phishing strategies more effectively than a single monolithic model.

Whether you are a security researcher looking for a baseline model or a developer integrating phishing detection into a larger pipeline, this project provides a robust, API-driven solution complete with performance monitoring.

## 🚀 Features

-   **Advanced Training Pipeline**: Automated workflow for data validation, transformation, and multi-model training.
-   **Granular Prediction**: Real-time classification of URLs using cluster-specific XGBoost models.
-   **Intelligent Clustering**: Utilizes **K-Means clustering** to group similar data points, optimizing model performance for specific data subsets.
-   **Ensemble Power**: Leverages **XGBoost**, a gradient boosting framework known for its speed and performance in classification tasks.
-   **Robust Validation**: Strict schema validation for both training and prediction data to prevent garbage-in-garbage-out.
-   **Performance Monitoring**: Integrated `Flask-MonitoringDashboard` for tracking API latency, utilization, and error rates.
-   **RESTful API**: Exposes clean `/train` and `/predict` endpoints for easy integration with other systems.

## 🛠️ Technology Stack

| Component | Technology | Description |
| :--- | :--- | :--- |
| **Language** | ![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white) | Core programming language. |
| **Web Framework** | ![Flask](https://img.shields.io/badge/Flask-000000?style=flat&logo=flask&logoColor=white) | Lightweight WSGI web application framework. |
| **ML Libraries** | ![Scikit-Learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat&logo=scikit-learn&logoColor=white) | Used for K-Means clustering and data preprocessing. |
| **Model** | ![XGBoost](https://img.shields.io/badge/XGBoost-EB3429?style=flat&logo=xgboost&logoColor=white) | High-performance gradient boosting library. |
| **Data Processing** | ![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=white) | Data manipulation and analysis. |
| **Database** | ![SQLite](https://img.shields.io/badge/SQLite-07405E?style=flat&logo=sqlite&logoColor=white) | Serverless database for data validation and staging. |

## 📂 Project Structure

```
Phishing_Classifier/
├── DataTransformation_Prediction/   # 🔄 Transformations for prediction data
├── DataTransform_Training/          # 🔄 Transformations for training data
├── DataTypeValidation_Insertion_Prediction/ # 🛡️ Schema validation for prediction
├── DataTypeValidation_Insertion_Training/   # 🛡️ Schema validation for training
├── Training_Raw_data_validation/    # 📁 Raw data validation logic
├── application_logging/             # 📝 Custom logging module
├── best_model_finder/               # 🧠 Logic to find the best model (XGBoost vs others)
├── data_ingestion/                  # 📥 Data loading modules
├── data_preprocessing/              # 🧹 Cleaning and preprocessing logic
├── file_operations/                 # 💾 Model saving/loading operations
├── prediction_Validation_Insertion.py # 🚦 Entry point for prediction validation
├── training_Validation_Insertion.py   # 🚦 Entry point for training validation
├── trainingModel.py                 # 🤖 Core model training logic
├── predictFromModel.py              # 🔮 Core prediction logic
├── main.py                          # 🚀 Flask application entry point
├── requirements.txt                 # 📦 Project dependencies
└── manifest.yml                     # ☁️ Deployment configuration
```

## ⚙️ Installation

1.  **Clone the repository**
    ```bash
    git clone https://github.com/Arnab-Ghosh7/Phising_Classifier.git
    cd Phising_Classifier
    ```

2.  **Create a virtual environment (Recommended)**
    ```bash
    python -m venv venv
    # Windows
    venv\Scripts\activate
    # Linux/Mac
    source venv/bin/activate
    ```

3.  **Install dependencies**
    ```bash
    pip install -r requirements.txt
    ```

## 🚀 Usage

1.  **Start the Server**
    ```bash
    python main.py
    ```
    The application will launch on `http://localhost:5000`.

2.  **Access the Dashboard**
    Monitor performance and API usage metrics at: `http://localhost:5000/dashboard`

## 📡 API Endpoints

### 1. Train Model
`POST /train`
Initiates the full training pipeline.
*   **Body**:
    ```json
    {
        "folderPath": "path/to/training_batch_files"
    }
    ```

### 2. Predict
`POST /predict`
Generates predictions for a batch of data.
*   **Body**:
    ```json
    {
        "folderPath": "path/to/prediction_batch_files"
    }
    ```

## 📊 Data Schema
The model relies on a robust set of features extracted from URLs. The schema (`schema_training.json`) validates these inputs.

**Key Features Include:**
- `having_IP_Address`: Checks if IP is used instead of domain.
- `URL_Length`: Length of the URL.
- `Shortining_Service`: Usage of TinyURL or similar services.
- `having_At_Symbol`: Presence of `@` symbol.
- `double_slash_redirecting`: Redirection using `//`.
- `Prefix_Suffix`: Domain contains `-`.
- `SSLfinal_State`: HTTPS status.
- `Domain_registeration_length`: How long the domain has been registered.
- `Favicon`: Presence of favicon.
- `port`: Non-standard ports.
- `HTTPS_token`: HTTPS in domain part.

## Author
Arnab Ghosh

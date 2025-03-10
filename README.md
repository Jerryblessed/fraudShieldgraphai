# FraudShield: AI-Powered Fraud Detection System

## Overview
FraudShield leverages AI-driven graph analytics to detect fraudulent activities, ranking threats via GPU-accelerated PageRank. It enables real-time monitoring, NLP-driven risk analysis, and intelligent mitigation.

## Architectural Diagram
```
+----------------------+     +---------------------+     +---------------------+
|  User Input (NLP)   | --> | Azure OpenAI (GPT)  | --> | AQL Query Generator |
+----------------------+     +---------------------+     +---------------------+
          |                              |                             |
          v                              v                             v
+----------------------+     +---------------------+     +---------------------+
|  ArangoDB Storage   | <-> | cuGraph Analytics   | <-> |  Graph Visualization |
+----------------------+     +---------------------+     +---------------------+
```
## Installation of Test Python Script
1. Clone the repository:
   ```sh
   git clone https://github.com/your-repo/fraudshield.git
   cd fraudshield
   ```
2. Install dependencies:
   ```sh
   pip install -r requirements.txt
   ```
3. Download and extract the dataset:
   ```sh
   wget --content-disposition "https://www.kaggle.com/api/v1/datasets/download/fraud-detection-dataset"
   unzip fraud-detection-dataset.zip
   ```
4. Set up environment variables:
   ```sh
   export DATABASE_HOST=<ArangoDB_Host>
   export DATABASE_USERNAME=<Your_Username>
   export DATABASE_PASSWORD=<Your_Password>
   export OPENAI_API_KEY=<Your_Azure_OpenAI_Key>
   ```

## Installation of Jupyter Notebook
1. Clone the repository:
   ```sh
   git clone https://github.com/your-repo/fraudshieldai.git
   cd fraudshield
   ```
2. Install dependencies within the notebook:
   ```sh
   Run the notebook cells line by line, starting from connecting to Colab and then using `!pip install` to install dependencies.
   ```
3. Download and extract the dataset within the notebook:
   ```python
   !wget --content-disposition "https://www.kaggle.com/api/v1/datasets/download/fraud-detection-dataset"
   !unzip fraud-detection-dataset.zip
   ```
4. Set up environment variables:
   ```python
   import os
   os.environ['DATABASE_HOST'] = '<ArangoDB_Host>'
   os.environ['DATABASE_USERNAME'] = '<Your_Username>'
   os.environ['DATABASE_PASSWORD'] = '<Your_Password>'
   os.environ['OPENAI_API_KEY'] = '<Your_Azure_OpenAI_Key>'
   ```

## Important Note on API Keys
The **Azure OpenAI API key** has been **intentionally left for testing purposes**. However, to ensure security and avoid unauthorized usage, **users who wish to test the system must renew the ArangoDB credentials from the temporary cloud version**.

To obtain new ArangoDB storage credentials, visit:  
[ArangoDB Cloud Connector](https://github.com/arangodb/adb-cloud-connector?tab=readme-ov-file#arangodb-cloud-connector)

## Getting ArangoDB Temporary Storage Credentials
To obtain temporary credentials for ArangoDB storage, visit:
[ArangoDB Cloud Connector](https://github.com/arangodb/adb-cloud-connector?tab=readme-ov-file#arangodb-cloud-connector)

## Usage
1. Run the application:
   ```sh
   python main.py
   ```
2. Query the system for fraudulent activities:
   ```sh
   python query.py "Find the most suspicious transactions"
   ```

## Features
- **AI-powered Fraud Detection**: Uses GPT-based NLP to analyze financial transactions.
- **Graph-based Risk Analysis**: Employs ArangoDB and cuGraph for advanced fraud analytics.
- **Real-time Monitoring**: Tracks and updates fraudulent activities dynamically.
- **Interactive Visualization**: Displays fraud intelligence insights in an intuitive manner.

## Future Improvements
- Integration with real-time transaction monitoring feeds.
- Support for additional anomaly detection models.
- Enhanced visualization with interactive dashboards.

## Contributing
Contributions are welcome! Feel free to fork the repo and submit pull requests.

## License
This project is licensed under the MIT License.


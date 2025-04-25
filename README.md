# 🐍 Customer Satisfaction Predictor

A machine learning pipeline system that predicts customer satisfaction scores for e-commerce orders before they happen.

## Project Overview 🔍

This project leverages the Brazilian E-Commerce Public Dataset by Olist to predict customer satisfaction scores based on order features like status, price, payment, and delivery performance. Built with ZenML, the system creates production-ready ML pipelines that continuously improve prediction accuracy.

## System Architecture 🏗️

The system consists of several key components:

- **ZenML Pipelines** 🔄: Orchestrates the entire ML workflow
- **MLflow Integration** 📊: Handles experiment tracking and model deployment
- **Streamlit Application** 💻: Provides a user interface for real-time predictions

## Features ✨

- **End-to-end ML Pipeline** 🔄: From data ingestion to model deployment
- **Automated Model Training** 🧠: Pipeline for continuous model improvement
- **Model Tracking** 📝: Comprehensive logging of metrics and parameters
- **Deployment Automation** 🚀: Automatic model deployment when quality thresholds are met
- **Interactive UI** 🖥️: Streamlit interface for making predictions
- **Reproducible Workflows** 🔁: Consistent, tracked ML processes

## Getting Started 🚀

### Prerequisites

- Python 3.7+
- Git

### Installation

```bash
# Clone the repository
git clone https://github.com/zenml-io/zenml-projects.git
cd zenml-projects/customer-satisfaction

# Install dependencies
pip install -r requirements.txt

# Install ZenML server dependencies
pip install zenml["server"]

# Install required ZenML integrations
zenml integration install mlflow -y
```

### Setting up ZenML Stack

```bash
# Start the ZenML server and dashboard
zenml up

# Register the required components
zenml experiment-tracker register mlflow_tracker --flavor=mlflow
zenml model-deployer register mlflow --flavor=mlflow
zenml stack register mlflow_stack -a default -o default -d mlflow -e mlflow_tracker --set
```

## Running the Pipelines 🏃‍♂️

### Training Pipeline

The training pipeline ingests data, cleans it, trains a model, and evaluates performance:

```bash
python run_pipeline.py
```

### Deployment Pipeline

The deployment pipeline extends the training pipeline and implements continuous deployment:

```bash
python run_deployment.py
```

### Streamlit Application

The Streamlit app provides a user interface to interact with the deployed model:

```bash
streamlit run streamlit_app.py
```

## Pipeline Details 📋

### Training Pipeline Steps

1. **Ingest Data** 📥: Loads and prepares the dataset
2. **Clean Data** 🧹: Preprocesses and transforms features
3. **Train Model** 🏋️‍♂️: Trains the prediction model
4. **Evaluation** 📏: Calculates and logs performance metrics

### Deployment Pipeline Steps

Includes all training pipeline steps, plus:

1. **Deployment Trigger** 🔍: Checks if the model meets quality thresholds
2. **Model Deployer** 🚀: Deploys the model as a service using MLflow

## Troubleshooting 🔧

### Common Issues

- **MLflow Deployer Not Found**: Delete the artifact store and rerun:
  ```bash
  zenml artifact-store describe  # Find the location
  rm -rf PATH  # Carefully delete it
  ```
  
- **Missing Environment Component**: Install the MLflow integration:
  ```bash
  zenml integration install mlflow -y
  ```

# End-to-End-Chest-Cancer-Classification-Project

## Project Structure
```
├───.github
│   └───workflows
├───config
├───research
├───src
│   ├───cnnClassifier
│   │   ├───components
│   │   ├───config
│   │   ├───constants
│   │   ├───entity
│   │   ├───logging
│   │   ├───pipeline
│   │   ├───utils
```
The project structure is organized as follows:

- `config.yaml`: Configuration file that contains project-specific settings and parameters.
- `research`: Contains notebook experiments which were performed before modular code implementation
- `params.yaml`: Parameter file that stores model-specific parameters and configurations.
- `entity`: Directory containing entity definitions and related files.
- `src/config`: Directory containing the configuration manager for accessing project configurations.
- `components`: Directory containing various components used in the text summarization pipeline.
- `pipeline`: Directory containing the main text chest cancer pipeline implementation.
- `main.py`: Main script that orchestrates the text summarization process.
- `.github/workflows`:Contains code for CICD .

## Pipelines
1. `stage_01_data_ingestion.py`: Sets up a configuration manager, reads project configurations, manages data ingestion settings, and provides functions to download and extract data from a remote source if it's not already available locally. It ensures that the necessary directories are created and errors are handled gracefully.
  
2. `stage_02_data_validation.py`: It ensures that the required files for data validation exist in the specified directory. The validation status is then written to a status file. Thus purpose of this data validation pipeline is to check whether the necessary data files are available before further processing or model training.

3. `stage_03_data_transformation.py` : It performs data transformation using a tokenizer from the transformers library and saves the transformed dataset to disk for later use during model training or evaluation in the chest cancer project. 

4. `stage_04_model_trainer.py` : It sets up the model and trainer for model training using the CNN model and saves the trained model

6. `stage_05_model_evaluation.py` : It evaluates a trained Pegasus model on a test dataset, calculates ROUGE scores and saves the scores to a CSV file for analysis in the chest cancer project. Note that this evaluation is performed on a small subset of the test dataset (first 10 examples) for demonstration purposes. In practice, it is common to evaluate the model on the entire test dataset. 


## Getting Started

To get started with the project, please follow these steps:

1. Clone the repository:
```
git clone https://github.com/SulemanZeb/End-to-End-Chest-Cancer-Classification-Project.git
```

2. Create a conda environment and activate it:
```
conda create -p cancer python==3.8 
conda activate cancer
```

3. Install the required dependencies:
```
pip install -r requirements.txt
```

## Workflows

1. Modify `config.yaml`
2. Modify `secrets.yaml` (if needed)
3. Modify `params.yaml`
4. Adjust the entity
5. Update the configuration manager in `src/config`
6. Adjust the components
7. Modify the pipeline
8. Edit `main.py`
9. Edit `dvc.yaml`



## MLflow

- [Documentation](https://mlflow.org/docs/latest/index.html)

- [MLflow tutorial](https://youtube.com/playlist?list=PLkz_y24mlSJZrqiZ4_cLUiP0CBN5wFmTb&si=zEp_C8zLHt1DzWKK)

##### cmd
- mlflow ui


### DVC cmd

1. dvc init
2. dvc repro
3. dvc dag


## About MLflow & DVC

MLflow

 - Its Production Grade
 - Trace all of your expriements
 - Logging & taging your model


DVC 

 - Its very lite weight for POC only
 - lite weight expriements tracker
 - It can perform Orchestration (Creating Pipelines)



# AWS-CICD-Deployment-with-Github-Actions

## 1. Login to AWS console.

## 2. Create IAM user for deployment

	#with specific access

	1. EC2 access : It is virtual machine

	2. ECR: Elastic Container registry to save your docker image in aws


	#Description: About the deployment

	1. Build docker image of the source code

	2. Push your docker image to ECR

	3. Launch Your EC2 

	4. Pull Your image from ECR in EC2

	5. Lauch your docker image in EC2

	#Policy:

	1. AmazonEC2ContainerRegistryFullAccess

	2. AmazonEC2FullAccess

	
## 3. Create ECR repo to store/save docker image
    - Save the URI: 566373416292.dkr.ecr.us-east-1.amazonaws.com/chicken

	
## 4. Create EC2 machine (Ubuntu) 

## 5. Open EC2 and Install docker in EC2 Machine:
	
	
	#optinal

	sudo apt-get update -y

	sudo apt-get upgrade
	
	#required

	curl -fsSL https://get.docker.com -o get-docker.sh

	sudo sh get-docker.sh

	sudo usermod -aG docker ubuntu

	newgrp docker
	
# 6. Configure EC2 as self-hosted runner:
    setting>actions>runner>new self hosted runner> choose os> then run command one by one


# 7. Setup github secrets:

    AWS_ACCESS_KEY_ID=

    AWS_SECRET_ACCESS_KEY=

    AWS_REGION = us-east-1

    AWS_ECR_LOGIN_URI = demo>>  566373416292.dkr.ecr.ap-south-1.amazonaws.com

    ECR_REPOSITORY_NAME = simple-app


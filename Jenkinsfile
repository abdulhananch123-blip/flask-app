pipeline {
    agent any

    environment {
        VENV = "venv"
        DEPLOY_DIR = "D:\\temp\\flask_deploy"
    }

    stages {

        stage('Clone Repository') {
            steps {
                echo "Cloning GitHub repository..."
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                echo "Installing Python dependencies..."
                bat '''
                python -m venv %VENV%
                %VENV%\\Scripts\\python -m pip install --upgrade pip
                %VENV%\\Scripts\\pip install -r requirements.txt
                '''
            }
        }

        stage('Run Unit Tests') {
            steps {
                echo "Running unit tests with pytest..."
                bat '''
                %VENV%\\Scripts\\pytest
                '''
            }
        }

        stage('Build Application') {
            steps {
                echo "Building application..."
                bat '''
                if not exist build mkdir build
                copy *.py build
                copy requirements.txt build
                '''
            }
        }

        stage('Deploy Application (Simulated)') {
            steps {
                echo "Simulating deployment..."
                bat '''
                if not exist %DEPLOY_DIR% mkdir %DEPLOY_DIR%
                xcopy build %DEPLOY_DIR% /E /Y
                '''
            }
        }
    }

    post {
        success {
            echo "Pipeline completed successfully!"
        }
        failure {
            echo "Pipeline failed. Check logs for errors."
        }
    }
}

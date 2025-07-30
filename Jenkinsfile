pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/shreya-singh27/Jenkins-Ansible-CI-CD.git'
        IMAGE_NAME = 'flask-app'
    }

    stages {
        stage('Clone Repo') {
            steps {
                echo 'Cloning the repository...'
                checkout([$class: 'GitSCM', branches: [[name: '*/main']],
                    userRemoteConfigs: [[url: "${REPO_URL}"]]])
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing Python and Docker if not installed...'
                sh '''
                    echo "Python version: $(python3 --version)"
                    echo "Pip version: $(pip3 --version)"
                    echo "Docker version: $(docker --version)"
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                sh '''
                    cd flask-app
                    docker build -t ${IMAGE_NAME} .
                '''
            }
        }

        stage('Run Container') {
            steps {
                echo 'Running Docker container...'
                sh '''
                    docker run -d -p 5000:5000 --name flask-container ${IMAGE_NAME}
                '''
            }
        }
    }

    post {
        success {
            echo 'CI/CD Pipeline executed successfully!'
        }
        failure {
            echo 'CI/CD Pipeline failed.'
        }
    }
}


pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "flask-app:latest"
    }

    stages {
        stage('Clone Repo') {
            steps {
                echo "Cloning the repository..."
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                echo "Installing Python and Docker if not installed..."
                sh '''
                which python3 || sudo apt-get install -y python3
                which pip3 || sudo apt-get install -y python3-pip
                which docker || curl -fsSL https://get.docker.com | sh
                pip3 install ansible
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "Building Docker image using Ansible playbook..."
                sh '''
                ansible-playbook ansible/playbook.yml -i ansible/inventory
                '''
            }
        }

        stage('Run Container') {
            steps {
                echo "Running container (handled in playbook)..."
            }
        }
    }

    post {
        success {
            echo ' CI/CD Pipeline executed successfully!'
        }
        failure {
            echo ' CI/CD Pipeline failed.'
        }
    }
}


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

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                sh '''
                    docker rm -f flask-container || true
                    docker rmi -f ${IMAGE_NAME} || true
                    cd flask-app
                    docker build -t ${IMAGE_NAME} .
                '''
            }
        }

        stage('Save Docker Image') {
            steps {
                echo 'Saving image as flask-app.tar...'
                sh '''
                    docker save -o flask-app/flask-app.tar ${IMAGE_NAME}
                '''
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                echo 'Running Ansible playbook to copy and run image on EC2...'
                sh '''
                    ansible-playbook -i ansible/inventory ansible/playbook.yml
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}


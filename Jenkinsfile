pipeline {
    agent any

    environment {
        REMOTE_USER = 'ubuntu'
        REMOTE_HOST = '3.109.55.203'
        IMAGE_NAME = 'flask-app'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/shreya-singh27/Jenkins-Ansible-CI-CD.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME ./flask-app'
            }
        }

        stage('Save Docker Image as TAR') {
            steps {
                sh 'docker save $IMAGE_NAME -o flask-app.tar'
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                sh '''
                    cd ansible
                    ansible-playbook -i inventory playbook.yml
                '''
            }
        }
    }
}


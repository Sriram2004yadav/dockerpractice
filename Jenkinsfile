pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')
        IMAGENAME = 'sriram040/flaskapp'
        GITREPO = 'https://github.com/Sriram2004yadav/dockerpractice'
        BRANCH = 'main'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning the repository...'
                git branch: "${BRANCH}", url: "${GITREPO}"
            }
        }

        stage('Build Image') {
            steps {
                echo 'Building Docker image...'
                bat "docker build -t ${IMAGENAME} ."
            }
        }

        stage('Push Image') {
            steps {
                echo 'Pushing Docker image to Docker Hub...'
                bat "docker login -u ${DOCKERHUB_CREDENTIALS_USR} -p ${DOCKERHUB_CREDENTIALS_PSW}"
                bat "docker push ${IMAGENAME}"
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline executed successfully!'
        }
        failure {
            echo '❌ Pipeline failed.'
        }
    }
}

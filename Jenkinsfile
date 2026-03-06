pipeline {
    agent any

    environment {
        IMAGE_NAME = 'jenkins-lab'
    }

    parameters {
        string(name: 'DEPLOY_ENV', defaultValue: 'staging', description: 'Môi trường deploy')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME} ."
            }
        }

        stage('Run Container') {
            steps {
                sh "docker run --rm ${IMAGE_NAME}"
            }
        }
    }

    post {
        success {
            echo "✅ Build thành công trên ${params.DEPLOY_ENV}"
        }
        failure {
            echo "❌ Build thất bại, kiểm tra lại log!"
        }
    }
}

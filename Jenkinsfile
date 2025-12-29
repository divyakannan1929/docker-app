pipeline {
    agent any

    environment {
        IMAGE_NAME = "simple-nginx-app"
        IMAGE_TAG  = "v${BUILD_NUMBER}"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git 'https://github.com/your-org/simple-docker-app.git'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t $IMAGE_NAME:$IMAGE_TAG .'
            }
        }

        stage('Docker Run') {
            steps {
                sh '''
                  docker rm -f nginx-demo || true
                  docker run -d -p 8081:80 \
                  --name nginx-demo \
                  $IMAGE_NAME:$IMAGE_TAG
                '''
            }
        }
    }

    post {
        success {
            echo "Application deployed successfully"
        }
        failure {
            echo "Pipeline failed"
        }
    }
}

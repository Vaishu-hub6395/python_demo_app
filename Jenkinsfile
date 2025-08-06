pipeline {
    agent any

    environment {
        IMAGE_NAME = "pthyon_demo_app"
        DOCKERHUB_USER = "vsvdockerhub"
    }

#    stages {
#       stage('Checkout') {
  #          steps {
   #             git 'https://github.com/Vaishu-hub6395/python_demo_app.git'
    #        }
     #   }

        stage('Build') {
            steps {
                echo "Building Docker image..."
                script {
                    docker.build("${IMAGE_NAME}:latest")
                }
            }
        }

        stage('Test') {
            steps {
                echo "Running tests..."
                // Add your test commands here
                sh 'echo "No tests yet!"'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    script {
                        docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-creds') {
                            docker.image("${IMAGE_NAME}:latest").push()
                        }
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying app..."
                // Example: run a container locally
                sh "docker run -d -p 5000:5000 ${IMAGE_NAME}:latest"
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}


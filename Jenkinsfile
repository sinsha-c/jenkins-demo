pipeline {
    agent any

    stages {
        stage('Check Docker Installation') {
            steps {
                echo "Checking Docker"
                sh '''
                    docker --version
                '''
            }
        }

        stage('Pull Redis Image') {
            steps {
                echo "Pulling Redis Docker Image"
                sh '''
                    docker pull redis
                '''
            }
        }

        stage('List Docker Images') {
            steps {
                echo "Displaying Docker Images"
                sh '''
                    docker images
                '''
            }
        }

        stage('Remove Existing Container') {
            steps {
                echo "Removing Old Redis Container"
                sh '''
                    docker rm -f redis-container || true
                '''
            }
        }

        stage('Run Redis Container') {
            steps {
                echo "Starting Redis Container"
                sh '''
                    docker run -d \
                        --name redis-container \
                        -p 6379:6379 \
                        redis
                '''
            }
        }

        stage('Check Running Container') {
            steps {
                echo "Checking Running Containers"
                sh '''
                    docker ps
                '''
            }
        }

        stage('Check Redis Logs') {
            steps {
                echo "Displaying Redis Logs"
                sh '''
                    docker logs redis-container
                '''
            }
        }
    }

    post {
        success {
            echo "Redis Container Started Successfully"
        }
        failure {
            echo "Pipeline Failed"
        }
        always {
            echo "Pipeline Execution Completed"
        }
    }
}

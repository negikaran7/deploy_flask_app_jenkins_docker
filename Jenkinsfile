pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'flask_app'
        REPO_URL = 'https://github.com/negikaran7/deploy_flask_app_jenkins_docker.git'
    }
   stages {
        stage('Checkout') {
            steps {
                // Checkout the source code from GitHub
                git url: "${REPO_URL}", branch: 'main'
            }
        }

        stage('Build') {
            steps {
                dir('flask app') {
                    script {
                        // Build Docker image
                        docker.build("${DOCKER_IMAGE}")
                    }
                }
            }
        }

        stage('Create Container') {
            steps {
                dir('flask app') {
                    script {
                        // Create and run Docker container
                        sh 'docker run -d -p 8181:8181 --name flask_app ${DOCKER_IMAGE}'
                    }
                }
            }
        }

        stage('Access Container') {
            steps {
                script {
                    // Access the Docker container
                    sh 'docker ps -a'
                    sh 'docker logs flask_app'
                }
            }
        }
    }

    // post {
    //     always {
    //         script {
    //             // Cleanup Docker images and containers
    //             sh 'docker rm -f flask_app || true'
    //             sh 'docker rmi $(docker images -q) || true'
    //         }
    //     }
    // }
}

pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'doanthinh2389/flask-app'
        DOCKER_TAG = 'latest'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/doanthinh2389/flask-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}:${DOCKER_TAG}")
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    sh 'docker stop flask-app || true'
                    sh 'docker rm flask-app || true'

                    docker.image("${DOCKER_IMAGE}:${DOCKER_TAG}").run(
                        "--name flask-app -p 5000:5000 -d"
                    )
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline hoàn thành!'
        }
    }
}

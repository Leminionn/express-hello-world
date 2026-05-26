pipeline {
    agent any

    environment {
        IMAGE_NAME = 'devops'
    }

    stages {
        stage('Checkout source code') {
            steps {
                checkout scm
            }
        }

        stage('Install dependencies') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'npm install'
                    } else {
                        bat 'npm install'
                    }
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'npm test'
                    } else {
                        bat 'npm test'
                    }
                }
            }
        }

        stage('Build docker image') {
            steps {
                script {
                    def imageTag = "${env.IMAGE_NAME}:${env.BUILD_NUMBER}"

                    if (isUnix()) {
                        sh "docker build -f dockerfile -t ${imageTag} ."
                    } else {
                        bat "docker build -f dockerfile -t ${imageTag} ."
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Thong bao: CI pipeline thanh cong.'
        }
        failure {
            echo 'Thong bao: CI pipeline that bai.'
        }
    }
}

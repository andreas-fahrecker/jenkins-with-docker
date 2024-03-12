#!groovy

pipeline {
    agent none

    stages {
        stage('Build/Push Docker Image') {
            when {
                beforeAgent true;
                branch 'main'
            }
            agent {
                label 'linux'
            }
            environment {
                DOCKER_HUB_CREDENTIALS = credentials('docker-hub-fah16145')
            }
            stages {
                stage('Default Image') {
                    stages {
                        stage('Build') {
                            steps {
                                sh 'docker build -t fah16145/jenkins-with-docker:latest .'
                            }
                        }
                        stage('Login') {
                            steps {
                                sh 'docker login -u ${DOCKER_HUB_CREDENTIALS_USR} -p ${DOCKER_HUB_CREDENTIALS_PSW}'
                            }
                        }
                        stage('Push') {
                            steps {
                                sh 'docker push fah16145/jenkins-with-docker:latest'
                            }
                        }
                    }
                }
                stage('Alpine Image') {
                    stages {
                        stage('Build') {
                            steps {
                                sh 'cd alpine'
                                sh 'docker build -t fah16145/jenkins-with-docker:alpine .'
                            }
                        }
                        stage('Push') {
                            steps {
                                sh 'docker push fah16145/jenkins-with-docker:alpine'
                            }
                        }
                    }
                }
            }
            post {
                always {
                    sh 'docker logout'
                }
            }
        }
    }
}

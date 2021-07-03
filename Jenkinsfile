
pipeline {
    agent any 

    environment {
        DOCKERHUB_CRED = credentials('DOCKER_HUB_CRED')
        REGISTRY_NAME = "supoodocker/my-app"
    }

    stages {
        stage('Build App') {
            steps {  
                dir("app") {
                     withGradle {
                        sh './gradlew build'
                    }
                }
            }
        }

        stage('Docker Login') {
            steps {  
               sh 'docker login --username $DOCKERHUB_CRED_USR --password-stdin'
            }
        }

        stage('Docker Build') {
            steps {  
               sh 'docker build -t $REGISTRY_NAME .'
            }
        }

        stage('Docker Push') {
            steps {  
               sh 'docker push $REGISTRY_NAME:latest'
            }
        }
    }
    post {
        always {
            sh 'docker logout'
        }
    }
}

pipeline {
    agent any 

    environment {
        DOCKERHUB_CRED = credentials('DOCKER_HUB_CRED')
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

        stage('Docker Push') {
            steps {  
               sh 'docker push supoodocker/my-app:latest'
            }
        }
    }
    post {
        always {
            sh 'docker logout'
        }
    }
}
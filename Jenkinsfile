
pipeline {
    agent any 

    environment {
        registryCredential = 'DOCKER_HUB_CRED'
        registry = "supoodocker/my-app"
        dockerImage = ''
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

        // stage('Docker Login') {
        //     steps {  
        //        sh 'docker login --username $DOCKERHUB_CRED_USR --password-stdin'
        //     }
        // }

        stage('Docker Build') {
             steps {
                sh 'docker build -t $registry .'
             }
        }

        // stage('Docker Push') {
        //         script { 
        //             docker.withRegistry( '', registryCredential ) { 
        //                 dockerImage.push() 
        //             }
        //         }
        // }
    }
    post {
        always {
            sh 'docker logout'
        }
    }
}
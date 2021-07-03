
pipeline {
    agent any

    environment {
        registryCredential = 'DOCKER_HUB_CRED'
        registry = "supoodocker/my-app"
        dockerImage = ''
    }

    stages {
        // stage('Build App') {
        //     steps {  
        //         dir("app") {
        //              withGradle {
        //                 sh './gradlew build'
        //             }
        //         }
        //     }
        // }

        stage('Build') {
            agent {
                docker {
                    image 'gradle:7.0.2-jdk11'
                    // Run the container on the node specified at the top-level of the Pipeline, in the same workspace, rather than on a new node entirely:
                    reuseNode true
                }
            }
            steps {
                sh 'gradle --version'
            }
        }

        // stage('Docker Login') {
        //     steps {  
        //        sh 'docker login localhost:8080'
        //     }
        // }

        // stage('Docker Build') {
        //      steps {
        //         sh 'pwd'
        //         sh 'docker build -t $registry .'
        //      }
        // }

        // stage('Docker Push') {
        //         script { 
        //             docker.withRegistry( '', registryCredential ) { 
        //                 dockerImage.push() 
        //             }
        //         }
        // }
    }
    // post {
    //     always {
    //         sh 'docker logout'
    //     }
    // }
}
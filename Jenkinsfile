
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

        stage('Docker Build') {
             steps {
                sh 'pwd'
                sh 'docker build -t $registry:latest .'
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
    // post {
    //     always {
    //         sh 'docker logout'
    //     }
    // }
}
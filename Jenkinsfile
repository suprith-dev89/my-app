
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
                 dir("app") {
                    //  sh 'pwd'
                    //  sh 'docker build -t $registry:latest .'
                    dockerImage = docker.build registry + ":$BUILD_NUMBER" 
                 }  
             }
        }

        stage('Docker Push') {
            steps {
                script { 
                    docker.withRegistry( '', registryCredential ) { 
                        //dockerImage.push() 
                        dockerImage.push($BUILD_NUMBER)            
                        dockerImage.push("latest")  
                    }
                } 
            }
        }
    }
    // post {
    //     always {
    //         sh 'docker logout'
    //     }
    // }
}

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
                     sh 'docker build -t $registry:latest .'
                     sh 'docker build -t $registry + ":$BUILD_NUMBER" .'
                 }  
             }
        }

        stage('Docker Push') {
            when {
                branch 'main'
            }
            steps {
                withDockerRegistry([ credentialsId: registryCredential, url: "" ]) {
                    sh 'docker push $registry:latest'
                    sh 'docker push $registry + ":$BUILD_NUMBER"'
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
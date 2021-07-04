
pipeline {
    agent any

    environment {
        //DockerHub
        REGISTRY_CRED = 'DOCKER_HUB_CRED'
        REGISTRY_NAME = "supoodocker/my-app"
        //GKE
        GKE_PROJECT_ID = "rosy-sunspot-318805"
        GKE_CLUSTER_NAME = "ssk-cluster-1"
        GKE_LOCATION = "us-central1-c"
        GKE_CREDENTIALS_ID = 'gke'
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
                     sh 'docker build -t $REGISTRY_NAME:latest .'
                     sh 'docker build -t $REGISTRY_NAME:$BUILD_NUMBER .'
                 }  
             }
        }

        stage('Docker Push') {
            steps {
                withDockerRegistry([ credentialsId: REGISTRY_CRED, url: "" ]) {
                    sh 'docker push $REGISTRY_NAME:latest'
                    sh 'docker push $REGISTRY_NAME:$BUILD_NUMBER'
                }
            }
        }

        stage('Deploy to GKE') {
            steps{
                withCredentials([file(credentialsId: "${GKE_CREDENTIALS_ID}", variable: 'JENKINSGCLOUDCREDENTIAL')])
                {
                    sh """
                        gcloud auth activate-service-account --key-file=${JENKINSGCLOUDCREDENTIAL}
                        gcloud config set compute/zone asia-southeast1-a
                        gcloud config set compute/region asia-southeast1
                        gcloud config set project ${GKE_PROJECT_ID}
                        gcloud container clusters get-credentials ${GKE_CLUSTER_NAME}

                        kubectl get pods

                        gcloud auth revoke --all
                        """
                }
            }
    }
}
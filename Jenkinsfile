
pipeline {
    agent any 
    stages {
        stage('build') {
            steps {  
                dir("app") {
                    echo "Build Started"
                    sh "gradle build"
                    echo "Build Completed"
                }
            }
        }
    }
}
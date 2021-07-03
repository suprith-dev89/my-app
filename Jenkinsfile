
pipeline {
    agent any 
    stages {
        stage('build') {
            steps {  
                dir("app") {
                    echo "Build Started"
                    sh "./gradlew -g /cache build"
                    echo "Build Completed"
                }
            }
        }
    }
}
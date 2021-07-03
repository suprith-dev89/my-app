
pipeline {
    agent any 
    stages {
        stage('build') {
            steps {  
                dir("app") {
                     withGradle {
                        sh './gradlew build'
                    }
                }
            }
        }
    }
}
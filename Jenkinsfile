pipeline {
    agent any
    stages {

        stage('Clone Repo') {
          steps {
            sh 'rm -rf pipeline*'
            sh 'git clone https://github.com/JaswikTechnologies/pipeline.git'
            }
        }
    }
}  

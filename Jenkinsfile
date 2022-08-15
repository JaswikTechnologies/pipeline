pipeline {
    agent any
    stages {
        stage("git clone")
        {
            steps{

                sh 'rm -rf pipeline.*'
                sh 'git clone https://github.com/JaswikTechnologies/pipeline.git'

            }
            
        }
    }
}

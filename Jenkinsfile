pipeline {
    environment { 
3
        registry = "jaswiktechnologiesdocker/nginx" 
4
        registryCredential = 'dockerhub_id'  
6
    }
    agent any
    stages {
        stage("git clone")
        {
            steps{

                sh 'rm -rf pipeline*'
                sh 'git clone https://github.com/JaswikTechnologies/pipeline.git'

            }
            
        }

        stage('Build Docker Image') {
          steps {
            sh 'docker build -t jaswiktechnologiesdocker/nginx:${BUILD_NUMBER} .'
            }
        }

        stage('Push Image to Docker Hub') {
          steps {
            docker.withRegistry('', registryCredential ) { 

           sh    'docker push jaswiktechnologiesdocker/nginx:${BUILD_NUMBER}'
           }
          }
        }

        stage('Deploy to Docker Host') {
          steps {
            sh    'docker -H tcp://10.1.1.21:2375 stop masterwebapp1 || true'
            sh    'docker -H tcp://10.1.1.21:2375 run --rm -dit --name masterwebapp1 --hostname masterwebapp1 -p 8000:80 jaswiktechnologiesdocker/nginx:${BUILD_NUMBER}'
            }
        }

        stage('Check WebApp Rechability') {
          steps {
          sh 'sleep 10s'
          sh ' curl http://10.1.1.21:8000'
          }
        }

    }
}

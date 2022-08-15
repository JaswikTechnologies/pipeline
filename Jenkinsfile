pipeline {
    agent any
    environment { 
3
        registry = "jaswiktechnologiesdocker/nginx" 
4
        registryCredential = 'dockerhub_id'  
6
    }
    stages {
        stage("Enviornment")
        {
            steps{
               echo "-------------------------"
               echo "My credentials is $registryCredential"
               
            }
            }
   
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
            script { 
            docker.withRegistry('https://hub.docker.com/repository/docker/jaswiktechnologiesdocker/nginx', registryCredential ) { 
            }
            }
           sh    'docker push jaswiktechnologiesdocker/nginx:${BUILD_NUMBER}'
           
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

pipeline {
   agent any
   stages {
    
        stage('Clone Repo') {  
          steps {    
            sh 'rm -rf dockertest1'
            sh 'git clone https://github.com/madhubabu-cloud/dockertest1.git'
            }
        }
       
     
        stage('Build Docker Image') {
            steps { 
              sh 'cd /var/lib/jenkins/workspace/pipeline1/dockertest1'
              sh'cp  /var/lib/jenkins/workspace/pipeline1/dockertest1/* /var/lib/jenkins/workspace/pipeline1'
              sh 'docker build -t madhudev/pipelinetest:v1 .'
               }
        }
         
        stage('Push Image to Docker Hub') {
            steps  {
                  sh 'docker push madhudev/pipelinetest:v1'
              }
        }

        stage('Deploy to Docker Host') {
            steps  {
          sh 'docker -H tcp://3.109.108.228:2375 stop webapp1 '
          sh 'docker -H tcp://3.109.108.228:2375 run --rm -dit --name webapp1 --hostname webapp1 -p 9000:80  madhudev/pipelinetest:v1'
           }
        } 
        stage('Check WebApp Rechability') {
            steps  {
         sh 'sleep 10s'
          sh 'curl http://ec2-3-109-108-228.ap-south-1.compute.amazonaws.com:9000'
           }
         }
    }     
}

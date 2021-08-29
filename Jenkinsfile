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
              sh 'cd /var/lib/jenkins/workspace/pipeline2/dockertest1'
              sh'cp  /var/lib/jenkins/workspace/pipeline2/dockertest1/* /var/lib/jenkins/workspace/pipeline2'
              sh 'docker build -t madhudev/pipelinetest:v4 .'
               }
        }
         
        stage('Push Image to Docker Hub') {
            steps  {
                  sh 'docker push madhudev/pipelinetest:v4'
              }
        }

        stage('Deploy to Docker Host') {
            steps  {
          sh 'docker -H tcp://3.109.108.228:2375 stop webapp2 '
          sh 'docker -H tcp://3.109.108.228:2375 run --rm -dit --name webapp2 --hostname webapp2 -p 9005:80  madhudev/pipelinetest:v4'
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

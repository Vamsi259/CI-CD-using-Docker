pipeline {
    agent any
	
	  tools
    {
       maven "Maven"
    }
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/devops4solutions/CI-CD-using-Docker.git'
             
          }
        }
	 stage('Execute Maven') {
           steps {
             
                bat "mvn package"
          }
        }
        

  stage('Docker Build and Tag') {
           steps {
              
                bat 'docker build -t vamsi259:latest .' 
                bat 'docker tag samplewebapp vamsi259/samplewebapp:latest'
                //sh 'docker tag samplewebapp vamsi259/samplewebapp:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
          bat  'docker push vamsi259/samplewebapp:latest'
        //  sh  'docker push nikhilnidhi/samplewebapp:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                bat "docker run -d -p 8003:8080 vamsi259/samplewebapp"
 
            }
        }
 stage('Run Docker container on remote hosts') {
             
            steps {
                //sh "docker -H ssh://jenkins@172.31.28.25 run -d -p 8003:8080 nikhilnidhi/samplewebapp"
 
            }
        }
    }
	}
    

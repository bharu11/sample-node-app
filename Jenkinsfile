pipeline {
    agent any
    environment {
        AWS_ACCOUNT_ID="306549046766"
        AWS_DEFAULT_REGION="us-west-2"
        IMAGE_REPO_NAME="node-app"
    }
   
    stages {
        
        stage('Checkout from Git') {
            steps {
                git branch: 'master',
                credentialsId: 'git_creds',
                url: 'https://github.com/bharu11/sample-node-app.git'  
            }
        }
        
        stage('Building docker image') {
            steps {
              script {
                  
                 dockerImage = docker.build "node-app"
                  
                }
                
            }
        }
        
         stage('Pushing docker image') {
            steps {
              script{
                    docker.withRegistry('https://306549046766.dkr.ecr.us-west-2.amazonaws.com/cicd-bhargavi-02-gradle-sample', 'ecr:us-west-2:aws_creds') {
                      docker.image(IMAGE_REPO_NAME).push()
                    }
                }
            }
        }
    }
    
}

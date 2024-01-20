pipeline {
    agent { label "dev-server"}
    
    stages{
        stage("Code"){
            steps{
                git url: "https://github.com/LondheShubham153/node-todo-cicd.git", branch: "master"
                echo 'Code clone is done'
                
            }
        }
        
        stage("Buid and Test"){
            steps{
               sh "docker build -t node-app-test-new ." 
                echo 'Code build is done'
                
            }
        }
        
        
        stage("Scan image"){
            steps{
                echo 'Image scan is done'
                
            }
        }
        
        stage("Push"){
            steps{
                withCredentials([usernamePassword(credentialsId:"DockerHub",passwordVariable:"DockerHubPass",usernameVariable:"DockerHubUser")]){
                sh "docker login -u ${env.DockerHubUser} -p ${env.DockerHubPass}"
                sh "docker tag node-app-test-new:latest ${env.DockerHubUser}/node-app-test-new:latest"
                sh "docker push ${env.DockerHubUser}/node-app-test-new:latest"
                echo 'image push is done'
                } 
            }
        }
    
        stage("Deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
                echo 'Code deploy is done'
                
                
            }
        }
        
    }
    
}

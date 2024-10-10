pipeline {
    agent  any
    
    stages {
        
        stage("code"){
            steps{
                git url: "https://github.com/jegedeokiki/node-todo-cicd.git", branch: "master"
                echo 'bhaiyya code clone ho gaya'
            }
        }
        stage("build and test"){
            steps{
                sh "docker build -t jegedeokiki/image ."
                echo 'code build bhi ho gaya'
            }
        }
        stage("scan image"){
            steps{
                echo 'image scanning ho gayi'
            }
        }
        stage("push"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerhubPass",usernameVariable:"dockerhubUser")]){
                sh "docker login -u ${env.dockerhubUser} -p ${env.dockerhubPass}"
                sh "docker tag jegedeokiki/image jegedeokiki/image"
                sh "docker push jegedeokiki/image"
                echo 'image push ho gaya'
                }
            }
        }
        stage("deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
                echo 'deployment ho gayi'
            }
        }
    }
}

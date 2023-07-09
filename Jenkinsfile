pipeline {
    agent { label "agentkrish" }
    stages{
        stage("Clone Code"){
            steps{
                git url: "https://github.com/krishkprawat/node-todo-cicd", branch: "master"
            }
        }
        stage("Build and Test"){
            steps{
                sh "docker build . -t krishpauri/node-todo-cicd:latest"
                echo "build done"
            }
        }
        stage("Push to Docker Hub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/node-todo-cicd:latest"
                }
            }
        }
        stage("Deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}

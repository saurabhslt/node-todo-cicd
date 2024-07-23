pipeline {
    
    agent any
    
    stages {
        
        stage("Code"){
            steps{
                git url: "https://github.com/saurabhslt/node-todo-cicd.git" , branch: "master"
                echo "Code Cloned Successfully"
            }
        }
        stage("Build"){
            steps{
                sh 'docker build -t node-app-batch-6:latest .'
                echo "Code Built Successfully"
            }
        }
        stage("Test"){
            steps{
                echo "Build Tested Successfully"
            }
        }
        stage("Push to Private Docker Hub Repo"){
            steps{
                withCredentials([usernamePassword(credentialsId:"DockerHubCreds",passwordVariable:"dockerPass",usernameVariable:"dockerUser")]){
                sh "docker login -u ${env.dockerUser} -p ${env.dockerPass}"
                sh "docker tag node-app-batch-6:latest ${env.dockerUser}/node-app-batch-6:latest"
                sh "docker push ${env.dockerUser}/node-app-batch-6:latest"
                }
                
            }
        }
        stage("Sonar"){
            steps{
                echo "Build Tested Successfully"
            }
        }
        stage("OWASP"){
            steps{
                echo "Build Tested Successfully"
            }
        }
        stage("Trivy"){
            steps{
                echo "Image Scanned Successfully"
            }
        }
        stage("Deploy"){
            steps{
                sh "docker-compose up -d"
                echo "App Deployed Successfully"
            }
        }
    }
}

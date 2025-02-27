pipeline{
    
    agent any
    
    stages{
        stage("code"){
            steps{
                git( url: "https://github.com/nenisrudani7/online_shoping_ci_cd.git", branch: "Master" ,  credentialsId: 'github')
                echo "code done";
            }
        }
        stage("build"){
            steps{
                sh "docker build -t node_jenkins:latest ."
            }
        }
         stage("upload image to dockerhub"){
          steps{
            withCredentials([usernamePassword(
            credentialsId:"dockerhub",
            passwordVariable:"dockerHubPass",
            usernameVariable:"dockerHubUser")]){
            sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
            sh "docker image tag node_jenkins:latest ${env.dockerHubUser}/node_jenkins:latest"
            sh "docker push ${env.dockerHubUser}/node_jenkins:latest"
            }
  
          }
        }
        stage("Test"){
          steps{
                echo "test done";
          }
        }
        stage("Deploy"){
          steps{
              stage("Deploy"){
    steps{
        sh "docker compose down"
        sh "docker compose up -d --build"
        echo "Deploy done";
    }
}

          }
        }
    }
}

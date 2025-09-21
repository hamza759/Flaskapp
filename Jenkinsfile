pipeline {
    
    agent{ label "dev" };
    
    stages{
        stage("Code"){
            steps{
                git url:"https://github.com/LondheShubham153/two-tier-flask-app.git", branch:"master"
            }
        }
        stage("Build"){
            steps{
                sh "docker build -t two-tier-flask-app ."
            }
        }
        stage("Test"){
            steps{
                echo "developer test lihk ky dy ga"
            }
        }
        stage("push to docker hub"){
            steps{
                withCredentials([usernamePassword(
                    credentialsId:"demohub",
                    passwordVariable:"dockerHubPass",
                    usernameVariable:"dockerHubUser"
                    )]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker image tag two-tier-flask-app ${env.dockerHubUser}/two-tier-flask-app"
                sh "docker push ${env.dockerHubUser}/two-tier-flask-app:latest"
            }
            }
        }
        stage("Deploy"){
            steps{

                sh "docker compose up -d --build flask-app"
           }
        }
    }
post 
    {
        success{
            emailext(
            subject: "build successfull",
            body: "your CICD build was successfull",
            to: 'ha1257656@gmail.com'
            )
        }
        failure{
            emailext(
            subject: "build Failed",
            body: "your CICD build got an error!",
            to: 'ha1257656@gmail.com'
            )
        }
    }
}

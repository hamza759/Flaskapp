@Library("Shared") _
pipeline {
    
    agent{ label "dev" };
    
    stages{
        stage("Code"){
            steps{
                script{
                     clone("https://github.com/hamza759/Flaskapp.git","main")
                }
            }
        }
        
        stage("Trivy File System Scane"){
            steps{
                script{
                 trivy_fs()    
                }
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
             script{
                 docker_push("demohub","two-tier-flask-app")
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
            script{
                emailext(
                from: 'ha1257656@gmail.com',
                to: 'hamzz7002@gmail.com',
                body: "your CICD build was successfull",
                subject: "CICD build successfully"
                    )
            }
        }
        failure{
            script{
                emailext(
                from: 'ha1257656@gmail.com',
                to: 'hamzz7002@gmail.com',
                body: "your CICD build got an error",
                subject: "CICD build failed"
                    )
            }
        }
    }
}

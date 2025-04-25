@Library("shared") _
pipeline{
    agent{label "vinod" }    
    stages{
        stage("Hello"){
            steps{
                script{ 
                    hello()
                }
            }
        }
        stage("Code"){
            steps{
                script{
                    clone("https://github.com/ChaitanyaKasar/django-notes-app.git", "main")
                }
            }
        }
        stage("Build"){
            steps{
               script{
                    docker_build("notes-app","latest","ckasar2708")  
               }
            }
        }
        stage("Push to DockerHub"){
            steps{
                script{
                     docker_push("notes-app","latest","ckasar2708")
                 }
                }
            }
        stage("Deploy"){
            steps{
                echo "This is deploying the code"
                sh '''
                    docker ps -q --filter ancestor=notes-app:latest | xargs -r docker rm -f
                    docker ps -q --filter "publish=8000" | xargs -r docker rm -f
                    docker run -d -p 8000:8000 notes-app:latest 
                '''
                
                // sh "docker compose down && docker compose up -d"
            }
        }
    }
}

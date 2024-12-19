@Library("Shared") _
pipeline {
    
    agent { label "vinod" }

    stages {
        
        stage('Hello') {
            steps {
                script{
                    hello()
                }
            }
        }
        
        stage('code') {
            steps {
                script{
                 sh 'sudo rm -rf workspace caches'
                 clone("https://github.com/abhinavm945/django-notes-app.git", "main")
                }
            }
        }
        
        stage('Build') {
            steps {
                script{
                docker_build("notes-app", "latest", "abhinavm945")
                }
            }
        }
        
        stage("Push to DockerHub") {
            steps {
                echo "This is pushing the image to Docker Hub"
                script{
                    docker_push("notes-app", "latest", "abhinavm945")
                }
            }
        }
        
        stage('Deploy') {
            steps {
                echo 'Deploying... the code'
                sh "docker compose down && docker compose up -d"
            }
        }
    }
}

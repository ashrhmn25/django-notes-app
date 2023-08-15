 pipeline {
    agent any 
    stages{
        stage("CLone Code"){
            steps {
                echo "Cloning the code"
                git url: "https://github.com/ashrhmn25/django-notes-app.git", branch: "main"
            }
        }
        stage("Build"){
            steps {
                echo "Building the image"
                sh "docker build . -t django-notes-app"
            }
        }
        stage("Push to dockerHub"){
            steps {
                echo "Pushing the image to dockerHub"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                    sh "docker tag django-notes-app ${env.dockerHubUser}/django-notes-app:latest"
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker push ${env.dockerHubUser}/django-notes-app:latest"
                }
            }
        }
        stage("Deploy"){
            steps {
                echo "Deploying the code"
                sh "docker-compose down"
                sh "docker-compose up -d"
                //sh "docker run -d -p 8000:8000 ashraf1980/django-notes-app:latest". Added
            }
        }
    }
}

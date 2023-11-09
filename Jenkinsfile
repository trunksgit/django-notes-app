pipeline {
    agent any

    stages {
        stage('Clone The Code') {
            steps {
                echo 'Cloing the Code'
                git branch: 'main', url: 'https://github.com/LondheShubham153/django-notes-app.git'
            }
        }
        stage('Build') {
            steps {
                echo 'Building the Code'
                sh 'docker build -t trunks-notes-app .'
            }
        }
        stage('Push to Docker Hub') {
            steps {
                echo 'Pushing the code to docker hub'
                withCredentials([usernamePassword(credentialsId: 'my-dockerhub-creds', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
                sh "docker tag trunks-notes-app ${env.dockerHubUser}/trunks-notes-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"   
                sh "docker push ${env.dockerHubUser}/trunks-notes-app:latest"
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying the Code'
                sh "docker-compose down && docker-compose up -d"
//              sh "docker run -d -p 8000:8000  sharkwave/trunks-notes-app:latest"
            }
        }
    }
}

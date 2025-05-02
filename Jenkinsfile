pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/aditya160403/simple-web-app.git', branch: 'main'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("simple-web-app:${BUILD_NUMBER}")
                }
            }
        }

        stage('Deploy Web App') {
            steps {
                script {
                    sh '''
                    docker stop simple-web-app || true
                    docker rm simple-web-app || true
                    docker run -d --name simple-web-app -p 8080:80 simple-web-app:${BUILD_NUMBER}
                    '''
                }
            }
        }
    }
}
=

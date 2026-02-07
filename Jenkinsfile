pipeline {
    agent any

    stages {

        stage('Clone Code') {
            steps {
                echo 'Code already cloned by Jenkins'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t static-site:latest .'
            }
        }

        stage('Run Container Test') {
            steps {
                sh '''
                docker run -d -p 8082:80 static-site
                sleep 5
                docker ps
                '''
            }
        }

        stage('Cleanup Test Container') {
            steps {
                sh '''
                docker stop $(docker ps -q --filter ancestor=static-site)
                '''
            }
        }
    }
}

pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                git 'https://github.com/23MH1A1227/jenkins.git'
            }
        }

        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Stop & Remove Old Container') {
            steps {
                sh '''
                docker stop jaya || true
                docker rm jaya || true
                '''
            }
        }

        stage('Remove Old Image') {
            steps {
                sh '''
                docker rmi keerthi || true
                '''
            }
        }

        stage('Docker Image Build') {
            steps {
                sh 'docker build -t keerthi .'
            }
        }

        stage('Docker Deploy') {
            steps {
                sh 'docker run -d -p 8083:8080 --name jaya keerthi'
            }
        }
    }
}

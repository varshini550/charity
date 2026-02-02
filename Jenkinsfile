pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                git 'https://github.com/varshini550/charity.git'
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
                docker stop charity-webapp2 || true
                docker rm charity-webapp2 || true
                '''
            }
        }

        stage('Remove Old Image') {
            steps {
                sh '''
                docker rmi charity || true
                '''
            }
        }

        stage('Docker Image Build') {
            steps {
                sh 'docker build -t amazon .'
            }
        }

        stage('Docker Deploy') {
            steps {
                sh 'docker run -d -p 8095:8080 --name azure amazon'
            }
        }
    }
}

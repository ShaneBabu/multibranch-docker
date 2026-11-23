pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'docker build -t image2 .'
            }
        }
        stage ("Tag") {
            steps {
                sh 'docker tag image2 kedarmahesh/jobtrack'
            }
        }
        stage('Push') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'dockerhub') {
                        sh 'docker push kedarmahesh/jobtrack'
                    }
                }
            }
        }
        stage ("Deploy") {
            steps {
                sh 'docker run -itd --name bus-app -p 2222:80 kedarmahesh/jobtrack'
            }
        }
    }
}

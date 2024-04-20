pipeline { 
    environment {
        IMAGE = "krishnagopika4/demo-cicd-1903"
        registryCredential = 'dockerhub'
        dockerImage = ''
    }
    agent any 
    stages {
        stage('checkout') {
                steps {
                git branch: 'main',
                url: 'https://github.com/krishnagopika/1903-jenkins.git'
                }
        }
        stage('Build') {
            steps {
                script {
                    dockerImage = docker.build "${IMAGE}:latest"
                }
            }
        }

        stage('Push image to docker hub') {
            steps {
                    script {
                     docker.withRegistry( '', registryCredential ) { 
                        dockerImage.push() 
                     }
                }
            }
        }

        stage('run the docker container') {
            steps {
                sh 'docker run -d -p 80:80 --name demo-app ${IMAGE}:latest'
                sh 'sleep 10'
                sh 'docker ps'
                sh 'docker stop demo-app'
                sh 'docker rm demo-app'
                sh 'docker rmi ${IMAGE}:latest'
            }
        
        } 
    }
}

pipeline { 
    environment {
        IMAGE = "abinash8/myrepo"
        dockerImage = ''
    }
    agent any 
    stages {
        stage('checkout') {
                steps {
                git branch: 'main',
                url: 'https://github.com/Abinashkhuntia/jenkins_task_revature.git'
                }
        // }
        // stage('Build') {
        //     steps {
        //         script {
        //             dockerImage = docker.build "${IMAGE}:latest"
        //         }
        //     }
        // }

        // stage('Push image to docker hub') {
        //     steps {
        //             script {
        //              docker.withRegistry( '', registryCredential ) { 
        //                 dockerImage.push() 
        //              }
        //         }
        //     }
        }

        stage('run the docker container') {
            steps {
                echo "building the docker image..."
                withCredentials([usernamePassword(credentialsId: 'b4a8af34-f778-49ef-9c08-02a6ad8901e5', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                sh "docker build -t ${IMAGE}:lts ."
                sh "echo $PASS | docker login -u $USER --password-stdin"
                sh "docker push ${IMAGE}:lts"
                echo "running the docker container..."
                sh "docker pull ${IMAGE}:lts"
                sh "docker run -d -p 80:80 --name demoapp ${IMAGE}:lts"
                sh "sleep 10"
                sh "docker ps"
                sh "docker stop demoapp "
                sh "docker rm demoapp"
                sh "docker rmi ${IMAGE}:lts"

                }
            }
        
        } 
    }
}

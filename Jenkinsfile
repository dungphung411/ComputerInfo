IMAGE_REG = "docker.io"
IMAGE_REPO ="mdngphg411/docker2node"
IMAGE_TAG ="latest"
runninguser = 'root'


pipeline {
    agent { label 'Main'}  
    stages {
        stage('Gitcheck') {
            steps{
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/dungphung411/ComputerInfo.git'
                sh 'sudo pwd'
                sh 'chmod -R 777 /var/lib/jenkins/workspace/docker2node'
                echo 'Git check successfully'
            }
        }
        
        stage('Docker build') {
            steps{
               // sh 'sudo docker login -u your_user_name -p your_password' enter it and run, and dont reveal your username and password to public
                sh(script:""" sudo su  $runninguser -c  "docker build . --file  build/Dockerfile --tag ${IMAGE_REG}/${IMAGE_REPO}:${IMAGE_TAG}" """,label:'Build docker image from dockerfile')
                sh 'sudo docker image ls '
                sh 'docker builder prune -y || true '
            }
        }
        stage('Docker push') {
            agent {label 'Main'}
            steps{ 
                sh(script:""" sudo su  $runninguser -c 'sudo docker push ${IMAGE_REG}/${IMAGE_REPO}:${IMAGE_TAG}' """, label: 'push image to the dockerhub')
                echo ' Pushing successfully'
            }
        }
        stage('Docker pull') {
            agent { label '10.32.4.107' }
            steps{
                sh(script:""" sudo su - $runninguser -c  'sudo docker pull ${IMAGE_REPO}:${IMAGE_TAG}' """, label: 'Pull image by node Docker 10.32.4.107' )
                sh 'sudo docker image ls'
            }
        }
        stage('Docker deploy'){
            agent { label '10.32.4.107' }
            steps{
                sh(script:""" sudo su - $runninguser -c  'sudo docker run -d -p 5000:5000 --name Computercheck ${IMAGE_REPO}' """, label: 'Pull image by node Docker 10.32.4.107' )
                sh 'sudo docker ps -a '
            }
         }
    }
}
    
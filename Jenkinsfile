pipeline {
    agent any
    
    tools{
        
        jdk 'jdk17'
    }
    
    environment {
        
        SCANNER_HOME= tool 'sonar-scanner'
    }

    stages {
        stage('Git Checkout ') {
            steps {
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/dungphung411/ComputerInfo.git'
            }
        }
        
        stage('OWASP Dependency Check') {
            steps {
                dependencyCheck additionalArguments: ' --scan ./ ', odcInstallation: 'DP'
                    dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
                sh 'sudo cat dependency-check-report.xml'
            }
        }
        
        stage('Sonarqube Analysis') {
            steps {
                
                withSonarQubeEnv('sonar'){
                  sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=ComputerInfo \
                    -Dsonar.projectKey=DemoInfocheck ''' 
               }
                
               
            }
        }
        
        stage('Docker Build & Tag') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred') {
                        sh "make image"
                    }
                }
            }
        }

        stage('Trivy Image Scan') {
            steps {
                sh "trivy image -f table mdngphg411/dotnet-demoapp"
            }
        }
        
        stage('Docker Push') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred') {
                        sh "make push"
                    }
                }
            }
        }
        
        stage('Docker Deploy') {
            steps {
                sh "sudo docker run -d -p 5000:5000 mdngphg411/dotnet-demoapp"
            }
        }
        
        
    }
}

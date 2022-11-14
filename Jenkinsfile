pipeline {
    agent any
    environment {
     shubham_docker=credentials('shubham_docker')
}
    stages{
        
        stage('code checkout and stash repo containing Dockerfile and app.py file'){
            agent {
                label 'jennode'
            }
            
            steps{
                
                
                script{
                    git url: "https://github.com/shubhamsinglaip/Dockerfile-and-app.py.git"
                    stash 'source'
                                      
                }
            }
        }
        stage('Build Docker Image'){
            agent {
                label 'myfirstnode'
            }
            
            
            steps{
                
                script{
                    sh 'docker build -t shubham030899/docker-jenkins-integration .'                   
                }
            }
        }
        stage('Push Image to Dockerhub'){
            agent {
                label 'myfirstnode'
            }
            
            steps{
                script{       
                        sh 'docker login -u ${shubham_docker_USR} -p ${shubham_docker_PSW} '
                        sh 'docker push shubham030899/docker-jenkins-integration'
                }
            }
        }
        stage('Pull Image from Hub'){
            agent {
                label 'myfirstnode'
            }
            
            steps{
                script{       
                    sh 'docker pull shubham030899/docker-jenkins-integration'
                }
            }
        }
        stage('Start Container'){
            agent {
                label 'myfirstnode'
            }
            
            steps{
                script{
                    sh 'docker rm mycontainer'
                    sh 'docker run --name mycontainer shubham030899/docker-jenkins-integration'
                }
            }
        }
    }
}

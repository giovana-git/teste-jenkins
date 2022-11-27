pipeline {
    agent any

    // environment {
    //     registry = "giovanacosta/app-a"
    //     registryCredential = 'dockerhub'        
    // }

    stages {

        stage('Inicial') {
            steps {
                echo 'Iniciando a pipeline'
            }
        }

        // stage('Origem do GitHub') {
        //     steps {
        //         git url: 'https://github.com/giovana-git/teste-jenkins.git', branch: 'main'
        //     }
        // }

        stage('Build das imagens Docker') {
            steps {
                script {
                    dockerappa = docker.build("giovanacosta/app-a", '-f ./app-a/Dockerfile ./app-a')
                    dockerappb = docker.build("giovanacosta/app-b", '-f ./app-b/Dockerfile ./app-b')
                    dockerappc = docker.build("giovanacosta/app-c", '-f ./app-c/Dockerfile ./app-c')
                    dockerappd = docker.build("giovanacosta/app-d", '-f ./app-d/Dockerfile ./app-d')
                }
            }
        }

        stage('Push imagem para o DockerHub') {

            environment {
               registryCredential = 'dockerhub'
           }

            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        dockerappa.push('latest')
                        dockerappb.push('latest')
                        dockerappc.push('latest')
                        dockerappd.push('latest')
                    }
                }
            }
        }

        stage('Deploying App to Kubernetes') {
            steps {
                script {
                    sh kubectl apply -f deployments
                    sh kubectl apply -f services
                    sh kubectl appl -f ingress                   
                }
            }
        }
    }
}
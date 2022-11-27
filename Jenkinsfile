pipeline {
    agent any

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

            environment {
                tag_version = "${env.BUILD_ID}"
            }

            steps {
                script {
                    dockerappa = docker.build("giovanacosta/app-a:$tag_version", '-f ./app-a/Dockerfile ./app-a')
                    dockerappb = docker.build("giovanacosta/app-b:$tag_version", '-f ./app-b/Dockerfile ./app-b')
                    dockerappc = docker.build("giovanacosta/app-c:$tag_version", '-f ./app-c/Dockerfile ./app-c')
                    dockerappd = docker.build("giovanacosta/app-d:$tag_version", '-f ./app-d/Dockerfile ./app-d')
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
                        dockerappa.push('${env.BUILD_ID}')
                        dockerappb.push('${env.BUILD_ID}')
                        dockerappc.push('${env.BUILD_ID}')
                        dockerappd.push('${env.BUILD_ID}')
                    }
                }
            }
        }

        stage('Deploy no cluster') {
            steps {
                script {
                    sh kubectl apply -f deployments                 
                }
            }
        }
    }
}
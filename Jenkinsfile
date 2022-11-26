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

        stage('Origem do GitHub') {
            steps {
                git url: 'https://github.com/giovana-git/teste-jenkins.git', branch: 'main'
            }
        }

        // stage('Build') {
        //     steps {
        //         sh "docker build -t giovanacosta/app-a:latest ."
        //     }
        // }

        stage('Build das imagens Docker') {
            steps {
                script {
                    dockerappa = docker.build("giovanacosta/app-a", '-f ./workspace/pipe-kubernetes/teste-jenkins/app-a/Dockefile ./app-a')
                    // dockerappb = docker.build("giovanacosta/app-b", '-f ./Lab-Jenkins/app-b/Dockerfile ./Lab-Jenkins/app-a')
                    // dockerappc = docker.build("giovanacosta/app-c", '-f ./Lab-Jenkins/app-c/Dockerfile ./Lab-Jenkins/app-a')
                    // dockerappd = docker.build("giovanacosta/app-d", '-f ./Lab-Jenkins/app-d/Dockerfile ./Lab-Jenkins/app-a')
                }
            }
        }

        // stage('Push imagem para o DockerHub') {
        //     steps {
        //         script {
        //             docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
        //                 dockerappa.push('latest')
        //                 dockerappb.push('latest')
        //                 dockerappc.push('latest')
        //                 dockerappd.push('latest')
        //             }
        //         }
        //     }
        // }
        // stage('Deploying App to Kubernetes') {
        //     steps {
        //         script {
        //             kubernetesDeploy(configs: "deploymentservice.yml", kubeconfigId: "kubernetes"                    
        //         }
        //     }
        // }
    }
}
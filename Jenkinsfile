pipeline {
    environment {
        imagename = "amit14321/jenkins-javaapp-training"
        dockerImage = ''
        registryCredentials = 'dockerhub'
    }
    agent any
    tools {
        maven 'MVN3'
        dockerTool 'docker'
    }
    stages {
        stage("pullscm") {
            steps {
                git credentialsId: '13400340-94b4-4004-9e0a-d47507f91053', url: 'git@github.com:amit14321/javaapp-kuber.git'
            }
        }
        stage("build") {
            steps {
                sh "mvn -f kubernetes-java clean install"
            }
        }
        stage("Build Docker Image") {
            steps {
                script {
                    dockerImage = docker.build("$imagename", "kubernetes-java")
                }
            }
        }
        stage("Push Docker Image") {
            steps {
                script {
                    docker.withRegistry( '', registryCredentials ) {
                        dockerImage.push()
                    }
                }
            }
        }
        stage("Cleanup") {
            steps {
                sh "docker rmi $imagename"
            }
        }
        stage("pull repo on linux node"){
            agent {label 'linux'}
            steps{
                 git credentialsId: '13400340-94b4-4004-9e0a-d47507f91053', url: 'git@github.com:amit14321/javaapp-kuber.git'
            }
        }
        stage("kubedeployment"){
             agent {label 'linux'}
             steps{
                 sh "kubectl apply -f kubernetes-java/deploy.yml"
             }
        }
    }
}

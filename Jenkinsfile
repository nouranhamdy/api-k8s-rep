pipeline {
    agent any
    stages {
        stage('clone base repo'){
            steps{
                git 'https://github.com/nouranhamdy/api-k8s-rep.git'
            }
        }
        stage('clone kustomize repo'){
            steps{
                git 'https://github.com/nouranhamdy/kustomization.git'
            }
        }
        stage('deploy k8s resources'){
            steps{
                dir("${env.WORKSPACE}/environments/"){
                    sh 'kubectl apply -k ${params.namespace}'
                }
            }
        }
    }
}
pipeline {
    agent any
    stages {
        stage('clone base repo'){
            steps{
                git 'https://github.com/nouranhamdy/api-k8s-rep.git'
            }
        }
    
        stage('GitCheckout') {
            steps {
                checkout \
                    scm: [ $class : 'GitSCM', branches: [[name: '*/master']], extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'api-k8s-repo']], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/nouranhamdy/kustomization.git']]]
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
                    sh 'ls ../../base'
                    sh 'kubectl apply -k $namespace'
                }
            }
        }
    }
}
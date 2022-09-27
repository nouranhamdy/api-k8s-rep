pipeline {
    agent {label 'localhost'}
    stages {
        // configuring scm using jenkins syntax
        // 1- creates subdirectory in the workspace
        // 2- clone the git repo in that directory
        stage('GitCheckout') {
            steps {
                checkout \
                    scm: [ $class : 'GitSCM', branches: [[name: '*/master']], extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'api-k8s-repo']], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/nouranhamdy/api-k8s-rep.git']]]
            }
        }
        
        stage('GitCheckout 2') {
            steps {
                checkout \
                    scm: [ $class : 'GitSCM', branches: [[name: '*/master']], extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'environments']], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/nouranhamdy/kustomization.git']]]
            }
        }

        stage('deploy k8s resources'){
            steps{
                dir("${env.WORKSPACE}/environments/"){
                    sh 'ls ../api-k8s-repo'
                    sh 'kubectl apply -k $namespace'
                }
            }
        }
    }
}
pipeline {
    agent {label 'localhost'}
    stages {
        // configuring scm using jenkins syntax
        // 1- creates subdirectory in the workspace
        // 2- clone the git repo in that directory
        // stage('GitCheckout') {
        //     steps {
        //         checkout \
        //             scm: [ $class : 'GitSCM', branches: [[name: '*/master']], extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'base']], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/nouranhamdy/api-k8s-rep.git']]]
        //     }
        // }
        
        stage('GitCheckout 2') {
            steps {
                checkout \
                    scm: [ $class : 'GitSCM', branches: [[name: '*/master']], extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'environments']], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/nouranhamdy/kustomization.git']]]
            }
        }

        stage('deploy k8s resources'){
            steps{
                dir("${env.WORKSPACE}/environments/"){
                    sh 'cat $namespace/kustomization.tmpl'
                    //use envsubst for multiple variables substitution in one line 
                    sh '/usr/local/bin/envsubst < $namespace/kustomization.tmpl > $namespace/kustomization.yaml'
                    sh 'cat $namespace/kustomization.yaml'
                    sh '/usr/local/bin/kubectl apply -k $namespace'
                }
            }
        }
    }
}

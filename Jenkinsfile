pipeline {
    agent any
    tools {
        maven 'maven'
    }
    stages {
        stage ('build maven'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/GiriSurineni/devops-automation']])
                sh 'mvn clean install'
            }
        }
        stage ('build docker image'){
            steps{
                script{
                    sh 'docker build -t sgiriprasad/devops-integration .'
                }
            }
        }
        stage ('push image to hub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                    sh 'docker login -u sgiriprasad -p ${dockerhubpwd}'
}
                    sh 'docker push sgiriprasad/devops-integration'
                }
            }
        }
    }
}
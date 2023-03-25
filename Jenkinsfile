pipeline {
    agent any
    environment {
        //be sure to replace "bhavukm" with your own Docker Hub username
        DOCKER_IMAGE_NAME = "akhil322/train-schedule"
        GIT_BRANCH = "https://github.com/Akhil322/cicd-pipeline-train-schedule-autodeploy"
        IMAGE_NAME = "train-schedule"
    }
    stages {
        stage('Checkout') {
            steps {checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: GIT_BRANCH]]])
            }
        }
        stage('Build') {
            steps {
sh "ls -ltr"
sh "docker build -t akhil322/edureka:0.1 ."
sh "docker images"
            }
        }
        stage('Push') {
            steps {
sh "docker login -u akhil322 -p Akhil@322"
sh "docker push akhil322/edureka:0.1"
            }
        }
        stage("Deploy") {
            steps {
sh "kubectl replace -f train-schedule-kube.yml"
            }
        }
    }
}

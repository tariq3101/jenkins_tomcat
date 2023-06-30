pipeline {
    agent any

    stages {
        stage('GIT Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/devopsbyhari/JenkinsTomcatExample.git']])
            }
        }
        stage('Package') {
            steps {
                echo 'maven is packaging project'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying package into tomcat'
            }
        }
    }
}

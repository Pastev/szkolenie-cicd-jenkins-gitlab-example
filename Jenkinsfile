pipeline {
    agent any

    tools {
        maven "maven-3"
    }

    stages {
        stage('Clean') {
            steps {
                cleanWs()
            }
        }
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'git@github.com:Pastev/szkolenie-cicd-jenkins-gitlab-example.git'
            }
        }
        stage('Build') {
            steps {
                sh "mvn clean verify"
            }
            post {
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    slackSend channel: 'jenkins-przemek-piasta', message: "${env.BUILD_TAG} i ${env.BUILD_URL}"
                }
            }
        }
    }
}

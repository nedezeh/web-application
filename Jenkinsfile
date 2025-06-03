pipeline {
    agent any

    stages {
        stage('continuous download') {
            steps {
                echo 'echo downloading in progress'
                 git branch: 'main', url: 'https://github.com/nedezeh/web-application.git'
            }
        }
        stage('continuous build') {
            steps {
                echo 'echo building in progress'
                 sh 'mvn clean install'
            }
        }
        stage('continuous deployment') {
            steps {
                echo 'echo deploying application to PRODUCTION'
                 deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'tomcat', path: '', url: 'http://98.80.220.227:8080')], contextPath: 'my-webapp', war: '**/*.war'
            }
        }
        stage('continuous deployment') {
            steps {
                echo 'echo deploying application to TESTING'
                 deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'tomcat', path: '', url: 'http://34.236.171.35:8080')], contextPath: 'my-webapp', war: '**/*.war'
            }
        }
    }
}

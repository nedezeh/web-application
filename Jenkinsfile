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

        stage('deploy to Nexus Repository') {
            steps {
                echo 'Uploading build artifact to Nexus'
                withCredentials([usernamePassword(credentialsId: 'nexus', usernameVariable: 'NEXUS_USER', passwordVariable: 'NEXUS_PASS')]) {
                    sh """
                        mvn deploy -DskipTests=true \
                        -Dnexus.username=$NEXUS_USER \
                        -Dnexus.password=$NEXUS_PASS
                    """
                }
            }
        }

        stage('continuous deployment P') {
            steps {
                echo 'echo deploying application to PRODUCTION'
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'tomcat', path: '', url: 'http://44.192.93.77:8080')], contextPath: 'my-webapp', war: '**/*.war'
            }
        }

        stage('continuous deployment T') {
            steps {
                echo 'echo deploying application to TESTING'
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'tomcat', path: '', url: 'http://3.234.242.57:8080')], contextPath: 'my-webapp', war: '**/*.war'
            }
        }
    }
}

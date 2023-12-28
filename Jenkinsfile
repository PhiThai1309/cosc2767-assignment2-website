pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // Build Maven project
                sh 'mvn clean package'
            }
        }

        stage('Deploy') {
            steps {
                script {
                    deploy adapters: [tomcat9(credentialsId: 'tomcat_credential', path: '', url: 'http://34.227.79.199:8080')], contextPath: '/pipeline', onFailure: false, war: '**/*.war' 
                }
            }
        }
    }
} 
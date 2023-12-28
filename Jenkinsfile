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
                    deploy adapters: [tomcat9(credentialsId: 'tomcat_credential', path: '', url: 'http://3.83.102.118:8080')], contextPath: '/s3878070-website', onFailure: false, war: '**/*.war'
                }
            }
        }
    }
} 
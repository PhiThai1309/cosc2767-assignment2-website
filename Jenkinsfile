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
                    deploy adapters: [tomcat9(credentialsId: 'tomcat_credential', path: '', url: 'http://$IP_ADDRESS:8081')], contextPath: '/pipeline', onFailure: true, war: '**/*.war' 
                }
            }
        }
    }
} 
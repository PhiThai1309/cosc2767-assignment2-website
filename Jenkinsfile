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
                    def ipAddress = env.IP_ADDRESS
                    def tomcatUrl = 'http://' + ipAddress + ':8080'
                    deploy adapters: [tomcat9(credentialsId: 'tomcat_credential', path: '', url: tomcatUrl)], contextPath: '/pipeline', onFailure: false, war: '**/*.war' 
                }
            }
        }
    }
} 
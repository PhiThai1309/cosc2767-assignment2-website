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
                    def tomcatUrl = 'http://' + ipAddress + ':8081'
                    deploy adapters: [tomcat9(credentialsId: 'tomcat_credential', path: '', url: 'http://$env.IP_ADDRESS:8081')], contextPath: '/pipeline', onFailure: false, war: '**/*.war' 
                }
            }
        }
    }
} 
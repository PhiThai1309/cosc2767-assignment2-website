pipeline {
    agent any

    stages {
        //Build the project with maven
        stage('Build') {
            steps {
                // Build Maven project
                sh 'mvn clean package'
            }
        }

        //Deploy on Tomcat
        stage('Deploy') {
            steps {
                script {
                    // // Determine current IP address
                    // def currentIpAddress = sh(script: 'curl -s ifconfig.me', returnStdout: true).trim()

                    // Replace the placeholder IP address in the Tomcat URL
                    def tomcatUrl = "http://localhost:8081"

                    // Deploy to Tomcat with the updated URL
                    deploy adapters: [tomcat9(credentialsId: 'tomcat_credential', path: '', url: tomcatUrl)], contextPath: '/pipeline', onFailure: false, war: '**/*.war'

                    // deploy adapters: [tomcat9(credentialsId: 'tomcat_credential', path: '', url: 'http://44.204.41.28:8081')], contextPath: '/pipeline', onFailure: false, war: '**/*.war' 
                }
            }
        }
        
    }
}

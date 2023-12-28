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
                    //Get the env var name IP_ADDRESS
                    def ipAddress = env.IP_ADDRESS
                    //Concat with http and port number
                    def tomcatUrl = 'http://' + ipAddress + ':8080'
                    //Deploy war/ear to container feature with credentials
                    deploy adapters: [tomcat9(credentialsId: 'tomcat_credential', path: '', url: tomcatUrl)], contextPath: '/s3878070', onFailure: false, war: '**/*.war' 
                }
            }
        }
    }
} 
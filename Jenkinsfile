pipeline {
    agent any

    environment {
        IP_ADDRESS = "${env.IP_ADDRESS}"
    }

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
                    deploy adapters: [tomcat9(credentialsId: 'tomcat_credential', path: '', url: "http://${IP_ADDRESS}:8081")], contextPath: '/pipeline', onFailure: false, war: '**/*.war' 
                }
            }
        }
        
    }
}

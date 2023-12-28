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
                    deploy adapters: [tomcat9(credentialsId: 'tomcat_credential', path: '', url: 'http://$(curl -s ifconfig.me):8081')], contextPath: '/pipeline', onFailure: false, war: '**/*.war' 
                }
            }
        }
        
    }
}

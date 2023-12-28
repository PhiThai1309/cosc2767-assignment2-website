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
                    withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId:'IP_ADDRESS',
                    usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']
                    ])
                    deploy adapters: [tomcat9(credentialsId: 'tomcat_credential', path: '', url: 'http://$(env.USERNAME):8081')], contextPath: '/pipeline', onFailure: false, war: '**/*.war' 
                }
            }
        }
        
    }
}

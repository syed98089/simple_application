pipeline {
    agent any
       tools{
           maven "Maven"
              }
    stages {
        stage('Checkout') {
            steps {
              checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: '0fcc1a1d-40f1-44bc-ae80-3fab4010ceab', url: 'https://github.com/syed98089/simple_application.git']]])
                    }
                }
             
 
        stage('Build') {
            steps {    
                sh 'mvn clean package'       
                }
                }
             }
}

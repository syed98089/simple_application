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
             
 
        stage('Build for install artifact ') {
            steps {    
                sh 'mvn clean install'  
                }
                }
         stage('Build for package artifact') {
            steps {
                sh 'mvn clean package'
                }
                }

       
        stage('Deploy Artifact on Nexus') {
            steps {
                  script{
                      nexusArtifactUploader artifacts: [[artifactId: 'maven-project', classifier: '', file: '/var/lib/jenkins/workspace/build_job/webapp/target/webapp.war', type: 'war']], credentialsId: 'nexus3', groupId: 'com.example.maven-project', nexusUrl: '172.31.43.81:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'simpleapp-repo', version: '1.0.0'             
                }
                }
                }

}
}

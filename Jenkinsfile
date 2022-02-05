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

        stage('Deploy on Tomcat server') {
            steps {
                 sshagent(['deploy_user']) {
               sh 'scp  -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/build_job/webapp/target/webapp.war ec2-user@3.86.80.197:/opt/tomcat/apache-tomcat-8.5.75/webapps'
               
                }
                }
                }
       
        stage('Deploy Artifact on Nexus') {
            steps {
             nexusArtifactUploader artifacts: [[artifactId: 'maven-project', classifier: '', file: 'webapp.war', type: 'war']], credentialsId: 'nexus2', groupId: 'com.example.maven-project', nexusUrl: '172.31.81.22', nexusVersion: 'nexus2', protocol: 'http', repository: 'simple_app_release/', version: '1.0.0'
    
                }
                }

}
}

pipeline {
    // add your slave label name
    agent { label 'my-jenkins-slave'}
    tools{
        maven 'maven-test'
    }
    stages {
        stage ('Checkout_SCM') {

            steps {
          	    
	     checkout scm
            }
        }

        stage ('Maven_Build') {

            steps {
               sh 'mvn clean package'
            }
        }
        
        stage ('Deploy_Tomcat') {

            steps {
	      sshagent(['my-tomcat-server']) {
              sh "scp -o StrictHostKeyChecking=no  target/maven-web-application.war  ec2-user@52.66.135.19:/opt/tomcat9/webapps"
	      }
         }
        }
        
    }
}

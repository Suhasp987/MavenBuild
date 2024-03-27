pipeline {
    agent any
  tools{
      maven 'Maven3'
  }
    environment{
        JAVA_HOME ='C:\Program Files\Java\jdk-21'
    }
    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                bat 'mvn clean install -Dmaven.test.skip=true'
            }
        }
        
        stage('Test Cases Execution') {
            steps {
                bat 'mvn clean org.jacoco-maven-plugin:prepare-agent install -Pcoverage-per-test'
            }
        }
        
        
        
        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.war'
            }
        }
        
        stage('Deployment') {
            steps {
                deploy adapters: [tomcat9(credentialsId:'TomcatCreds',path:"",url:'http://localhost:8090/')],contextPath:'counterwebapp',war:'target/*.war'
            }
        }
        
        stage('Notification') {
            steps {
                emailext(
                    subject: "Job Completed",
                    body: "Jenkins Pipeline Job for Maven got completed!",
                    to: "suhas123.p@gmail.com"
                )
            }
        }
    }
}

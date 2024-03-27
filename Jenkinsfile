node(){
	stage('checkout code'){
		checkout scm
	}
	stage('Build'){
		sh "mvn clean install -Dmaven.test.skip=true"
	}
	stage('Test Cases Execution'){
		sh "mvn clean org.jacoco-maven-plugin:prepare-agent install -Pcoverage-per-test"
	}
	stage('Sonr Analysis'){
	}
	stage('Archieve Artifacts'){
		arcgieveArtifacts artifacts: 'target/*.war'
	}
	stage('Deployment'){
		deploy adapters: [tomcat9(credentialsId:'TomcatCreds',path:"",url:'http://localhost:8090/')],contextPath:'counterwebapp',war:'target/*.war'
	}
	stage('Notification'){
		emailext(
			subject:"Job Completed",
			body:"Jenkins Pipeline Job for Maven got completed!",
			to:"suhas123.p@gmail.com"
		)
	}
}

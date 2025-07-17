node{
    def mavenHome = tool name :'maven-3.9.10'
    stage('CheckoutCode'){
        git branch: 'development', changelog: false, credentialsId: 'd1ab30c6-ca84-433d-96b9-c69a9527a71c', 
        poll: false, url: 'https://github.com/uptimecarer/MBP-maven-web-application.git'
    }
    stage('MavenBuildArtifact'){
       sh "${mavenHome}/bin/mvn clean package"
    }
	stage('Sonarqube Report'){
	sh "${mavenHome}/bin/mvn clean sonar:sonar"
	}
	stage('UploadArtifactInToNexus'){
	sh "${mavenHome}/bin/mvn clean deploy"
	}
	stage('Deploy App into AppServer'){
	sshagent(['327ed8ea-a078-4e1e-8435-ba4738d26d4b']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.233.31.80:/opt/tomcat9/webapps/"
      }
	
	}
}

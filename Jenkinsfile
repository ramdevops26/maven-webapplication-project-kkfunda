node {
    
	// /var/lib/jenkins/tools/hudson.tasks.Maven_MavenInstallation/maven-3.9.9/
	
   // Define Maven tool from Jenkins global configuration
    def mavenHome = tool name: 'maven-3.9.9'

    stage('git checkkout') {
	
	    // Stage 1: Checkout source code from Git
	       
		  git branch: 'test', url: 'https://github.com/ramdevops26/maven-webapplication-project-kkfunda.git'
		} 
		
		// Stage 2: Build the application and package it (.war/.jar)

    stage('build') {
	       
		     sh "${mavenHome}/bin/mvn clean package" 
		} 	
 
     // Stage 3: Generate SonarQube Report 

    stage('SonarQube  Report') {
           sh "${mavenHome}/bin/mvn sonar:sonar"
		
		
	}
	
	   // Stage 4: Deploy to Nexus 
	   stage('Deploy to Nexus') {
	
                 sh "${mavenHome}/bin/mvn clean deploy"
                 }

     // Stage 5: Deploy to Tomcat 
     stage('Deploy to Tomcat') {
    echo "Deploying WAR file using curl..."

    sh """
        curl -u sai:password \
        --upload-file  /var/lib/jenkins/workspace/scripted-pipeline-web-app-deployment/target/maven-web-application.war \
        "http://16.4.79.52:8080/manager/text/deploy?path=/maven-web-application&update=true"
    """
}
}

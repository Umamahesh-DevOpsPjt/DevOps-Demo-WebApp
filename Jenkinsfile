pipeline {
         agent any
	 tools {
        // Note: this should match with the tool name configured in your jenkins instance (JENKINS_URL/configureTools/)
        maven 'Maven3.6.3'
   	 }
	 stages {
                 stage('Clone source') {
                 steps {
                      git url: 'https://github.com/Umamahesh-DevOpsPjt/DevOps-Demo-WebApp.git'
                 	}
                 }
		 
		 stage('Maven Build') {
                 steps {
                      sh 'mvn -Dmaven.test.failure.ignore=true clean package' 		      
                 	}
                 }
		 
	       //stage('SonarQube Analysis') {
                 //steps {
			// script{
			//   def scannerHome = tool 'sonarqube'
                         //   withSonarQubeEnv('sonarqube') { 
			  //  sh "${scannerHome}/bin/sonar-scanner -Dproject.settings=sonar-project.properties"
     			  //  sh 'mvn clean compile sonar:sonar -Dsonar.host.url=http://35.188.155.53:9000/ -Dsonar.sources=. -Dsonar.tests=. -Dsonar.test.inclusions=**/test/java/servlet/createpage_junit.java -Dsonar.exclusions=**/test/java/servlet/createpage_junit.java'
        		//	}
			   // }
			//}
              //  }
		
		 //stage('Quality Gate') {
			// steps{
			//	timeout(time: 10, unit: 'MINUTES') {
                           //    waitForQualityGate abortPipeline: true 
			//	}
			// }
		// }		 
		 
                 stage('Deploy to test') {
                  steps {
                  deploy adapters: [tomcat8(url: 'http://146.148.76.89:8080/', credentialsId: 'tomcat', path: '' )], contextPath: '/QAWebapp', war: '**/*.war'
	            }
                 }
		 
		 
		 stage('Deploy Artifact'){
			 steps{	
				 rtServer(
				id: 'artifactory',
   				 url: 'https://venkatdevops.jfrog.io/artifactory',
    
    				credentialsId: 'deploy',
    				// If Jenkins is configured to use an http proxy, you can bypass the proxy when using this Artifactory server:
    				bypassProxy: true,
    				// Configure the connection timeout (in seconds).
    				// The default value (if not configured) is 300 seconds:
    				timeout: 300    
					 )
			}
		 }
		 
		 
		 stage('UI Test'){
			 steps {
				 script{
					 def rtMaven = Artifactory.newMavenBuild()
					 def buildInfo
					 rtMaven.tool = "Maven3.6.3"
				 buildInfo = rtMaven.run pom: 'functionaltest/pom.xml', goals: 'test'
				 publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '\\functionaltest\\target\\surefire-reports', reportFiles: 'index.html', reportName: 'UI Test Report', reportTitles: ''])
				 }
			 }		 
		 }
		 
		 
		 stage('Performance Test') {
			 steps{
				 
			 
			 }
		 
		 }
            	        
               
	 }        	                       
}

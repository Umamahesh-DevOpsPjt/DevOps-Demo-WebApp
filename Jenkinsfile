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
		 
	//	stage('SonarQube') {
        //         steps {
        //            withSonarQubeEnv(credentialsId: 'sonar', installationName: 'sonarqube') { 
     	//		sh 'mvn clean package sonar:sonar -Dsonar.host.url=http://13.82.181.227:9000/ -Dsonar.sources=. -Dsonar.tests=. -Dsonar.test.inclusions=**/test/java/servlet/createpage_junit.java -Dsonar.exclusions=**/test/java/servlet/createpage_junit.java'
        //			}
	//		}
        //        }
		 
                 stage('Deploy to test') {
                 steps {
                  deploy adapters: [tomcat8(url: 'http://146.148.76.89:8080/', credentialsId: 'tomcat', path: '' )], contextPath: '/QAWebapp', war: '**/*.war'
	            }
                 }
		         	
            	        
               
	 }        	                       
}

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
		 
		stage('Sonarqube') {
   			 environment {
        			scannerHome = tool 'sonarqube'
   				     }
                steps {
                   withSonarQubeEnv('sonarqube') {
                    sh "${scannerHome}/bin/sonar-scanner"
                            }
                    timeout(time: 10, unit: 'MINUTES') {
                   waitForQualityGate abortPipeline: true
                         }
                    }
		}
		 
                 stage('Deploy to test') {
                 steps {
                  deploy adapters: [tomcat8(url: 'http://146.148.76.89:8080/', credentialsId: 'tomcat', path: '' )], contextPath: '/QAWebapp', war: '**/*.war'
	            }
                 }
		         	
            	        
               
	 }        	                       
}

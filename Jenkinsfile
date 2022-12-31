pipeline {
    agent any
	tools { 
        maven 'Maven_3_8_5'  
    }

    stages {
        stage('CompileandRunSonarAnalysis') {
            steps {	
		    withCredentials([string(credentialsId: 'sonarTokenId', variable: 'SONAR_TOKEN')]) {
				bat("mvn -Dmaven.test.failure.ignore verify sonar:sonar -Dsonar.login=$SONAR_TOKEN -Dsonar.projectKey=simplemavenproject -Dsonar.host.url=http://localhost:9000/")
		    }
			}
        } 
		stage('RunSCAAnalysisUsingSnyk') {
            steps {		
			//SNYK_TOKEN environment variable created on windows
				bat("mvn snyk:test -fn")
			}
        } 
		stage('RunDASTUsingZAP') {
            steps {		
				bat("D:\\software\\ZAP\\zap.sh -cmd -quickurl https://www.example.com -quickprogress -quickout D:\\software\\ZAP\\zap_reportOutput.html")
		  }
        } 
    }
}

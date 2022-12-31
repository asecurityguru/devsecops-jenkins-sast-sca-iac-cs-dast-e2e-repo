pipeline {
    agent any
	tools { 
        maven 'Maven_3_8_5'  
    }

    stages {
//        stage('CompileandRunSonarAnalysis') {
//             steps {	
// 		    //withCredentials([string(credentialsId: 'sonarTokenId', variable: 'SONAR_TOKEN')]) {
// 		//	bat("SET result=curl -s -u sqp_1cc89897a86cfbe98639d6847c6c5434ec2bd592: https://sonarcloud.io/api/qualitygates/project_status?projectKey=test")	

// 		    bat("mvn -Dmaven.test.failure.ignore verify sonar:sonar -Dsonar.login=sqp_1cc89897a86cfbe98639d6847c6c5434ec2bd592 -Dsonar.projectKey=test -Dsonar.host.url=http://localhost:9000/")
// 		    //}
// 			}
//         } 
// 		stage('RunSCAAnalysisUsingSnyk') {
//             steps {		
// 			//SNYK_TOKEN environment variable created on windows
// 				bat("mvn snyk:test -fn")
// 			}
//         } 
// 		stage('RunDASTUsingZAP') {
//             steps {		
// 				//bat("D:\\software\\ZAP\\zap.sh -cmd -quickurl https://www.example.com -quickprogress -quickout D:\\software\\ZAP\\zap_reportOutput.html")
// 		  }
//         } 
 	    		stage('RunDockerScan') {
             steps {		
	    bat("C:\\Users\\asecu\\AppData\\Local\\Programs\\Python\\Python311\\Scripts\\pip3 install --upgrade pip && C:\\Users\\asecu\\AppData\\Local\\Programs\\Python\\Python311\\Scripts\\pip3 install --upgrade setuptools && C:\\Users\\asecu\\AppData\\Local\\Programs\\Python\\Python311\\Scripts\\pip3 install checkov")
//	    bat("C:\\Users\\asecu\\AppData\\Local\\Programs\\Python\\Python311\\Scripts\\pip3pip3 install checkov")
// 				bat("docker scan --file Dockerfile openjdk:8-slim")
 		  }
         } 
	    		 stage('test') {
            steps {
              bat("checkov --file main.tf")
                }
            }
        
	
    }
}

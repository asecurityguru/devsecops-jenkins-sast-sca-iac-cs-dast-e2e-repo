pipeline {
    agent any
	tools { 
        maven 'Maven_3_8_5'  
     //   python 'python21'
    }

    stages {
       stage('CompileandRunSonarAnalysis') {
            steps {	
		    //withCredentials([string(credentialsId: 'sonarTokenId', variable: 'SONAR_TOKEN')]) {
		//	bat("SET result=curl -s -u sqp_1cc89897a86cfbe98639d6847c6c5434ec2bd592: https://sonarcloud.io/api/qualitygates/project_status?projectKey=test")	

		    bat("mvn -Dmaven.test.failure.ignore verify sonar:sonar -Dsonar.login=sqp_1cc89897a86cfbe98639d6847c6c5434ec2bd592 -Dsonar.projectKey=test -Dsonar.host.url=http://localhost:9000/")
		    //}
			}
        } 
// 	    stage('Build') { 
//             steps { 
//                withDockerRegistry([credentialsId: "dockerlogin", url: ""]) {
//                  script{
//                  app =  docker.build("asecurityguru/testeb")
//                  }
//                }
//             }
//     }
 		stage('RunContainerScan') {
            steps {		
			
	    withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
			
		    script{
		    try{
		    bat("C:\\snyk\\snyk-win.exe  container test asecurityguru/testeb")
		    }
		    catch(err) {
                echo err.getMessage()
            }
	    }
			}
		} 
		}
	    stage('RunSnykSCA') {
            steps {		
			
	    withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
				bat("mvn snyk:test -fn")
		} 
		}
	    }
		stage('RunDASTUsingZAP') {
            steps {		
				bat("C:\\zap\\ZAP_2.12.0_Crossplatform\\ZAP_2.12.0\\zap.sh -port 9393 -cmd -quickurl https://www.example.com -quickprogress -quickout C:\\zap\\ZAP_2.12.0_Crossplatform\\ZAP_2.12.0\\Output.html")
		  }
        } 

	    		 stage('checkov') {
            steps {
		
		    bat("checkov -s -f main.tf")
        
	    }
            }
	
        
	
    }
}

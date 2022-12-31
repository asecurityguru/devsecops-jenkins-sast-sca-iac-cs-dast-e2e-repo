pipeline {
    agent any
	tools { 
        maven 'Maven_3_8_5'  
    }
	 docker {
            image 'kennethreitz/pipenv:latest'
            args '-u root --privileged -v /var/run/docker.sock:/var/run/docker.sock'
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
// 	    		stage('RunDockerScan') {
//             steps {		
// 				bat("docker scan --file Dockerfile openjdk:8-slim")
// 		  }
//         } 
	    		 stage('test') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: 'master']], userRemoteConfigs: [[url: 'https://github.com/asecurityguru/devsecops-jenkins-sast-sca-iac-cs-dast-e2e-repo.git']]])
                script { 
                    sh """pipenv install
                    pipenv run pip install bridgecrew
                    pipenv run bridgecrew --directory . --bc-api-key 0e39afd7-c394-4210-86ad-49a6857a885a --repo-id asecurityguru/devsecops-jenkins-sast-sca-iac-cs-dast-e2e-repo"""
                }
            }
        }
	
    }
}

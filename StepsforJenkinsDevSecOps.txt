1) Create/Clone GitHub Repo
2) Jenkins, Docker should be installed
3) Download and run SonarQube image in Docker using commands:
      docker run -d --name sonarqube -p 9000:9000 -p 9092:9092 sonarqube
4) Setup Maven on windows
5) Define maven configuration in Jenkins
6) Create SNYK_TOKEN in windows
7) Install Python and set environment variable of scripts folder for pip
8) Install checkov using pip3
9) Install Terraform and set environment variable in windows
10) Install Python and do custom installation to install checkov using pip
11) Install fortify plugin in jenkins and then configure system - set trial.fortify.com
12) Create Personal access token in FOD and copy, username, tenant details and add in configure system (This will be setup in a script pipeline job and triggered separately
13) Download Snyk cli, place in a folder and run it for container scan

pip3 install --upgrade pip && pip3 install --upgrade setuptools
pip3 install checkov

docker scan --login
docker scan --file Dockerfile openjdk:8-slim


pipeline {
    agent {
        docker {
            image 'kennethreitz/pipenv:latest'
            args '-u root --privileged -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    stages {
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
    options {
        preserveStashes()
        timestamps()
    }
}
Copy
Learn more on Tech Docs


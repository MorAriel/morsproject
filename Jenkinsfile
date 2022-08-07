pipeline {

    agent any

    stages{
	    stage ('Workspace Cleanup') {
		steps {    
	    cleanWs()
          }	
	}
	    stage('Git Checkout') {
            steps {
		    git branch: 'main', url: 'https://github.com/MorAriel/morsproject.git'
            }
        }
        stage('build') {
            steps{
                sh "echo mors project"
		sh "pwd"   
		sh "ls"
                sh "docker build -t morsproject/$BUILD_NUMBER:v1 app1/"
                }
            }

        stage('push') {
            steps {
                sh "aws ecr get-login-password --region eu-central-1 | docker login --username AWS --password-stdin 557447257572.dkr.ecr.eu-central-1.amazonaws.com"
                sh "docker tag morsproject/$BUILD_NUMBER:v1 557447257572.dkr.ecr.eu-central-1.amazonaws.com/morsproject:$BUILD_NUMBER"
                sh "docker push 557447257572.dkr.ecr.eu-central-1.amazonaws.com/morsproject:$BUILD_NUMBER"
            }
        }

    }
}

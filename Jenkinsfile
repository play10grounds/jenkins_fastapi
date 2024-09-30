pipeline {
    agent any

	environment {
	    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
  		IMAGE_NAME="siestageek/jenkins_jodejs3"
  		IMAGE_TAG="latest"
	}

    stages {
        stage('clone from SCM') {
            steps {
                git url: 'https://github.com/play10grounds/jenkins_fastapi.git', branch: 'main'
            }
        }
		
		stage('Docker Building Node.js App') {
            steps {
                sh '''
        				docker compose build
        				'''
            }
        }
		
		stage('Logging into Docker Hub') {
            steps {
                sh '''
        				echo ${DOCKERHUB_CREDENTIALS_PSW} | docker login -u ${DOCKERHUB_CREDENTIALS_USR} --password-stdin
        				'''
            }
        }
		
		stage('Pushing Docker image to Docker Hub') {
            steps {
                sh '''
        				docker tag siestageek/nodejs-app ${IMAGE_NAME}:${IMAGE_TAG}
        				docker push ${IMAGE_NAME}:${IMAGE_TAG}
        				'''
            }
        }
		
		stage('Docker Hub logout') {
            steps {
                sh '''
        				docker logout
        				'''
            }
        }
		
    }
}

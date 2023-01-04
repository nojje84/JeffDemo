
pipeline{

   agent any

	//create dockerhub credential in github with TOKEN
	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub')
	}
	
	stages {

		stage('gitclone') {

		      steps {
		         git 'https://github.com/nojje84/JeffDemo.git'
		      }
		}
		
		stage('Build') {
			steps {
			
			   sh 'docker build -t nojje/class_app:${BUILD_NUMBER} .'
			}
		}
		
		stage('Login') {
		
			steps {
			   sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login --username nojje --password-stdin'    
			}
		}

		stage('Push') {
			
			steps {
			   sh 'docker push nojje/class_app:${BUILD_NUMBER}'
			}
		}
		}
	
	post {
	    always {
		sh 'docker logout'
	    }
    }

}

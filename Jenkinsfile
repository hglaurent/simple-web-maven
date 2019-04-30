pipeline {
    agent any
 
 	tools {
 		maven 'localMaven'
 	}
 
    stages{
        stage('Init') {
            steps {
                echo 'Testing...'
            }
        }
        stage('Build') {
            steps {
                echo 'Building...'
                bat 'mvn clean package'
            }
            post {
            	success {
            		echo 'Now archiving'
            		archiveArtifacts artifacts: '**/target/*.war'
            	}
            }
        }
       stage('Deploy to staging') {
            steps {
                echo 'Code Deployed...'
                build job: 'deploy-to-staging'
            }
        }
	
	      stage('Deploy to production') {
            steps {
	            timeout(time:5, unit:'DAYS') {
	            	input message:'Approve PRODUCTION Deployement?'
	            }
                build job: 'deploy-to-prod' 
            }
          
            post {
            	success {
            		echo 'code deployed to Production.'
            	}
            	failure {
                 	echo 'Deployment failed.'       	
            	}
            }
        }
	}

}
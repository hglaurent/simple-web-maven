pipeline {
    agent any
 
    stages{
        stage('Init') {
            steps {
                echo 'Testing...'
            }
        }
        stage('Build') {
            steps {
                //echo 'Building...'
                bat 'mvn clean package'
            }
            post {
            	success {
            		echo 'Now archiving'
            		archiveArtifacts artifacts: '**/target/*.War'
            	}
            }
        }
       stage('Deploy') {
            steps {
                echo 'Code Deployed...'
            }
        }
	}
}
pipeline {
	agent any
	
	stages{
		stage('Checkout Code'){
			steps{
				checkout scm
				}
			}
	stage('Build'){
		steps{
			bat "mvn clean install -Dmaven.test.skip=true"
		}
	}
	
	stage('Archive Artifact'){
		steps{
		archiveArtifacts artifacts:'target/*.war'
		}
	}
	stage('deployment'){
		steps{
		deploy adapters: [tomcat9(url: 'http://localhost:8090/', 
                              credentialsId: 'tomcatcred')], 
                     war: 'target/*.war',
                     contextPath: 'pipeline-demo'
		}
		
	}
  }
}

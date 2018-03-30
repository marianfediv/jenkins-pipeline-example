pipeline {
    agent any
	
	parameters {
        string(name: 'FAIL',     defaultValue: 'false', description: 'Whether to fail')
    }

    stages {
        stage ('Compile Stage') {

            steps {
			    // send build started notifications
                slackSend (color: '#FFFF00', message: "Compile Stage Started: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
                
				withMaven(maven : 'Maven') {
                    sh 'mvn clean compile'
                }
			}
        }

        stage ('Testing Stage') {

            steps {
			     // send build started notifications
                slackSend (color: '#FFFF00', message: "Testing Stage Started: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
				
                withMaven(maven : 'Maven') {
                    sh 'mvn test'
                }
            }
        }
    }
	
    post {
		success {
		  slackSend (color: '#00FF00', message: "Successful: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
		}

		failure {
		  slackSend (color: '#FF0000', message: "Failed: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
		}
  }
}
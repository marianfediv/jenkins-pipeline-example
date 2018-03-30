pipeline {
    agent any
	
	parameters {
        string(name: 'FAIL',     defaultValue: 'false', description: 'Whether to fail')
    }

    stages {
        stage ('Compile Stage') {

            steps {
			    // send build started notifications
                slackSend (color: '#FFFF00', message: "STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
                
				withMaven(maven : 'Maven') {
                    sh 'mvn clean compile'
                }
			}
        }

        stage ('Testing Stage') {

            steps {
			     // send build started notifications
                slackSend (color: '#FFFF00', message: "STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
				
                withMaven(maven : 'Maven') {
                    sh 'mvn test'
                }
            }
        }
    }
	
    post {
    success {
      slackSend (color: '#00FF00', message: "SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
    }

    failure {
      slackSend (color: '#FF0000', message: "FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
    }
  }
}
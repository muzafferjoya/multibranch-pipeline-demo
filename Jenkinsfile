pipeline{
    agent {
	docker {
	  image 'node:14.16.0'
	  args '-p 5000:5000'
	}
    }
    environment{
	CI = 'true'
	HOME = '.'
        npm_config_cache = 'npm-cache'	
    }
    stages{
	stage('Build'){
	  steps {
		sh 'npm install'
	  }
	}
	stage('Test'){
	  steps{
	    sh './jenkins/scripts/test.sh'
	  }
	}
	stage('Deliver for development') {
            when {
                branch 'development'
            }
            steps {
                sh './jenkins/scripts/deliver-for-development.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
        stage('Deploy for production') {
            when {
                branch 'production'
            }
            steps {
                sh './jenkins/scripts/deploy-for-production.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}

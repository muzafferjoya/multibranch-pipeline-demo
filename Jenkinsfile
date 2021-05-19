pipeline{
    agent {
	docker {
	  image 'node:14.16.0'
	  args '-p 3000:3000'
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
    }
}

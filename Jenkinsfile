pipeline {
	agent any
	stages {
		stage('Checkout SCM') {
			steps {
				git branch: 'master', credentialsId: 'e8492039-5ea1-40f2-9f4a-9ce7e2dc4ac1', url: 'https://github.com/yongyongjiejie/3103Jenkins.git'
			}
		}
 		stage('OWASP DependencyCheck') {
            		steps {
                		dependencyCheck additionalArguments: '--format HTML --format XML --suppression suppression.xml', odcInstallation: 'OWASP'
            		}
        	}
	}	
	post {
        	success {
            		dependencyCheckPublisher pattern: 'dependency-check-report.xml'
        	}
    }
}

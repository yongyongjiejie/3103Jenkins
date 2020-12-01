pipeline {
	agent any
	stages {
		stage('Checkout SCM') {
			steps {
				git branch: 'test', credentialsId: 'aa7ce681-cf84-4bb1-a1a6-a7012789b2ba', url: 'https://github.com/yongyongjiejie/simple-java-maven-app'
			}
		}
 		stage('OWASP DependencyCheck') {
            		steps {
                		dependencyCheck additionalArguments: '--format HTML --format XML', odcInstallation: 'Default'
            		}
        	}
	}	
	post {
        	success {
            		dependencyCheckPublisher pattern: 'dependency-check-report.xml'
        	}
    }
}

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
		stage('Install') {
			steps {
				sh 'composer install'
			}
		}
		stage('PHPunit') {
			steps {
                		sh"./vendor/bin/phpunit tests --log-junit logs/unitreport.xml -c tests/phpunit.xml tests"
            		}
		}
	}	
	post {
        	success {
            		dependencyCheckPublisher pattern: 'dependency-check-report.xml'
        	}
		always{
            		junit testResults: 'logs/unitreport.xml'
        	}
    	}
}

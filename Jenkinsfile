pipeline {
	agent any 
	environment {
		PATH = "/opt/apache-maven-3.6.1/bin:$PATH"
	}
	stages {
	 	stage('compile') {
			steps {
				echo "build compile"
				git url:'https://github.com/samal-tech/DevOpsClassCodes'
				sh 'mvn compile'
			}	
	    }
        stage ('code Analysis') {
			steps {
				echo "test code"
				sh 'mvn -P metrics pmd:pmd'
			}
			post {
				success {
					pmd canComputeNew: false, defaultEncoding: '', healthy: '', pattern: '**/pmd.xml', unHealthy: ''
				}
			}
		}
		stage ('unit test') {
			steps {
				echo "unit test"
				sh 'mvn test'
			}
			post {
				success {
					junit 'target/surefire-reports/*.xml'
				}
			}
		}
		stage ('code covarage') {
			steps {
				echo "code covarage"
				sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
			}
			post {
				success {
					cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: 'target/site/cobertura/coverage.xml', conditionalCoverageTargets: '70, 0, 0', failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false
				}
			}
		}
		stage ('packaging') {
			steps {
				echo "package creation"
				sh 'mvn package'
			}
		}
	}
}

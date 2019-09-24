pipeline {
	agent any 
	stages {
	 	stage('compile') {
			steps {
				withMaven(maven : 'MAVEN') {
					echo "build compile"
					git url:'https://github.com/samal-tech/DevOpsClassCodes'
					sh 'mvn compile'
				}
			}	
	    	}
        	stage ('code-Analysis') {
			steps {
				echo "test code"
				withMaven(maven : 'MAVEN') {
					sh 'mvn -P metrics pmd:pmd'
				}
			}
			post {
				success {
					pmd canComputeNew: false, defaultEncoding: '', healthy: '', pattern: '**/pmd.xml', unHealthy: ''
				}
			}
		}
		stage ('unit-test') {
			steps {
				echo "unit test"
				withMaven(maven : 'MAVEN') {
					sh 'mvn test'
				}
			}
			post {
				success {
					junit 'target/surefire-reports/*.xml'
				}
			}
		}
		stage ('code-covarage') {
			steps {
				echo "code covarage"
				withMaven(maven : 'MAVEN') {
					sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
				}
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
				withMaven(maven : 'MAVEN') {
					sh 'mvn package'
				}
			}
		}
	}
}

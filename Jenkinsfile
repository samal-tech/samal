pipeline {
	agent any 
	environment {
		PATH = "/opt/apache-maven-3.6.1/bin:$PATH"
	}
	stages {
	 	stage(‘compile’) {
	   steps {
				echo "build compile"
		git url:'https://github.com/samal-tech/DevOpsClassCodes'
		sh 'mvn compile'
			}	
	    }
	}
}

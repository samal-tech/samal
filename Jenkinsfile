pipeline {
	agent any
	stages {
		stage('compile') {
	   steps {
				echo "compile started"
			 git url : https://github.com/samal-tech/DevOpsClassCodes
			 sh 'mvn compile'
			}
		}
	}
}

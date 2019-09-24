pipeline {
	agent any 
	stages {
	 	stage(‘compile’) {
	   steps {
				echo "build compile"
		git url:'https://github.com/samal-tech/DevOpsClassCodes'
		sh label:'',script:'mvn compile'
			}	
	    }
	}
}

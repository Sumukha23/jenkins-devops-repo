//Scripted
node {
	echo "Build"
	echo "Test"
	echo "Integration Test"
	}
//Declarative
pipeline {
	agent  { docker {image 'maven:3.9.10'} }
	stages{
		stage('Build'){
			steps{
				echo "Build"
				sh "mvn --version"	
			}
		}
		stage('Test'){
			steps{
				echo "Test"
			}
		}
		stage('Integration Test'){
			steps{
				echo "Integration Test"
			}
		}
	}
	post {
		always {
			echo 'Im awesome'
		}
		success{
			echo 'I run when you are successfull'
		}
		failure{
		    echo 'I run when you are failure'
		}
	}

}
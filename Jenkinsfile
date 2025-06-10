//Scripted
// node {
// 	echo "Build"
// 	echo "Test"
// 	echo "Integration Test"
// 	}
//Declarative
pipeline {
	agent any
	// agent  { docker {image 'maven:3.9.9'} }
	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages{
		stage('Checkout'){
			steps{
				sh 'mvn --version'
				sh 'docker version'	
				echo "Build"
				echo "Path - $PATH"
				echo "BUILD_Number - $env.BUILD_NUMBER"
				echo "Build_id - $env.BUILD_ID"
				echo "Job_Name - $env.JOB_NAME"
				echo "Build_Tag - $env.BUILD_TAG"
				
			}
		}
		stage('Compile'){
			steps{
				sh "mvn clean compile"
			}
		}
		// stage('Test'){
		// 	steps{
		// 		sh "mvn test"
		// 	}
		// }
		stage('Integration Test'){
			steps{
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}
		stage('Package'){
			steps{
				sh "mvn package -DskipTests"
			}
		}
		stage('Build Docker Image'){
			steps{
				script {
					dockerImage = docker.build("sumukhabg23/currency-exchange-devops:${env.BUILD_TAG}")
				}
			}
		}
		stage('Push Docker Image'){
			steps{
				script{
					docker.withRegistry('', 'dockerhub'){dockerImage.push();
					dockerImage.push('latest');}
					
				}
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
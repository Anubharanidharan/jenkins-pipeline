pipeline{
	agent any 
	//agent { docker { image 'maven:3.6.3'} }
	//agent { docker { image 'node:13.8'} }
	environment {
		dockerhome = tool 'MyDocker'
		mavenhome = tool 'MyMaven'
		PATH ="$dockerhome/bin:$mavenhome/bin:$PATH"
	}
	stages {
		stage ('Checkout') {
			steps {
				sh 'mvn --version'
				//sh 'docker version'
				echo "Path -> $PATH"
				echo "Build" 
				echo "Build NUmber -> $env.BUILD_NUMBER"
				echo "Build Id -> $env.BUILD_ID"
				echo "Job Name -> $env.JOB_NAME"
				echo "Build Tag Name -> $env.BUILD_TAG"
				echo "Build URL -> $env.BUILD_URL" 
			}
		}
		stage ('Compile') {
			steps {
				sh "mvn clean compile" 
			}
		}
		stage ('Test') {
			steps {
				sh "mvn test " 
			}
		}
		stage ('Integration Test') {
			steps {
				sh "mvn failsafe:integration-test failsafe:verify  " 
			}
		}
	}
	post {
		always {
			echo "Im awesome, I run always"
		}
		success{
			echo "I run when you are success "
		}
		failure{
			echo " I run when you are fail"
		}
	}
}

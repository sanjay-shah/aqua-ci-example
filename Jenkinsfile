pipeline {
	environment {
		registry = "bitsanjay198/aqua-test"
		registryCredential = 'bitsanjay198'
		dockerImage = ''
	}
	agent any
	stages {
		stage('Cloning our Git') {
			steps {
				git 'https://github.com/sanjay-shah/aqua-ci-example.git'
			}
		}
		stage('Building our image') {
			steps {
				script {
					dockerImage = docker.build registry + ":$BUILD_NUMBER"
				}
			}
		}
		stage("Scan aqua-docker-test image using Aqua Scanner"){
			steps	{
				aqua customFlags: '', hideBase: false, hostedImage: '', localImage: registry + ":$BUILD_NUMBER", locationType: 'local', notCompliesCmd: '', onDisallowed: 'ignore', policies: '', register: false, registry: '', showNegligible: false
			}
		}
		stage('Push image') {
		    steps {
		        sh "echo `docker login -u bitSanjay198 -p xxxxxx && docker push $registry:$BUILD_NUMBER`"
		    }
		}
		stage('Cleaning up') {
			steps {
				sh "docker rmi $registry:$BUILD_NUMBER"
			}
		}
	}
}

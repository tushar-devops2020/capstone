pipeline {

	environment {
		registry = "tushardevops2020/capstone_udacity"
		registryCredential = ‘mydockerhub’
  }
	agent any
	stages {

		stage('Lint Test for HTML & Dockerfile ') {
			steps {
				sh 'tidy -q -e *.html'
				sh 'hadolint Dockerfile'
			}
		}
		
		stage('Build Docker Image') {
			steps {
				script {
					dockerImage = docker.build registry + ":$BUILD_NUMBER"
					
				}
			}
		}
		
		stage('Push Image To Dockerhub') {
			steps {
				script {
					docker.withRegistry( '', registryCredential ) {
					dockerImage.push()
					}
				}
			}
		}
		stage('Remove Unused docker image') {
			steps{
					sh "docker rmi $registry:$BUILD_NUMBER"
				}
			
		}
		stage('Set current kubectl context') {
			steps {
				withAWS(region:'us-west-2', credentials:'tusharc3') {
					sh '''
						kubectl config use-context arn:aws:eks:us-west-2:368648265814:cluster/capstoneAppcluster
					'''
				}
			}
		}

		stage('Deploy blue container') {
			steps {
				withAWS(region:'us-west-2', credentials:'tusharc3') {
					sh '''
						kubectl apply -f ./blue-controller.json
					'''
				}
			}
		}

		stage('Deploy green container') {
			steps {
				withAWS(region:'us-west-2', credentials:'tusharc3') {
					sh '''
						kubectl apply -f ./green-controller.json
					'''
				}
			}
		}

		stage('Create the service in the cluster, redirect to blue') {
			steps {
				withAWS(region:'us-west-2', credentials:'tusharc3') {
					sh '''
						kubectl apply -f ./blue-service.json
					'''
				}
			}
		}

		stage('Waiting for user approve') {
            steps {
                input "All Done ? Are we ready to redirect user traffic to green?"
            }
        }

		stage('Create the service in the cluster, redirect to green') {
			steps {
				withAWS(region:'us-west-2', credentials:'tusharc3') {
					sh '''
						kubectl apply -f ./green-service.json
					'''
				}
			}
		}

	}
}

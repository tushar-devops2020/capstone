pipeline {
	agent any
	stages {

		stage('Create kubernetes cluster On AWS EKS') {
			steps {
				withAWS(region:'us-west-2', credentials:'tusharc3') {
					sh '''
						eksctl create cluster \
						--name capstoneAppcluster \
						--version 1.14 \
						--nodegroup-name standard-workers \
						--node-type t2.small \
						--nodes 2 \
						--nodes-min 1 \
						--nodes-max 3 \
						--node-ami auto \
						--region us-west-2 \
						--zones us-west-2a \
						--zones us-west-2b \
						--zones us-west-2c \
					'''
				}
			}
		}

		

		stage('Create conf file cluster on AWS EKS') {
			steps {
				withAWS(region:'us-west-2', credentials:'tusharc3') {
					sh '''
						aws eks --region us-west-2 update-kubeconfig --name capstoneAppcluster
					'''
				}
			}
		}

	}
}

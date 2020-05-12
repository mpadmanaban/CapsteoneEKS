pipeline {
	agent any
	stages {	
		stage('Create bluecluster') {
			steps {
				withAWS(region:'us-east-2', credentials:'jenkins-aws') {
					sh '''
						eksctl create cluster \
						--name capstonebluecluster \						
						--nodegroup-name standard-workers \
						--node-type t2.small \
						--nodes 1 \
						--nodes-min 1 \
						--nodes-max 3 \						
					'''
				}
			}
		}

		stage('create bluecluster kubectl config') {
			steps {
				withAWS(region:'us-east-2', credentials:'jenkins-aws') {
					sh '''
						aws eks --region us-east-2 update-kubeconfig --name capstonebluecluster
					'''
				}
			}
		}
		
		stage('Create greencluster') {
			steps {
				withAWS(region:'us-east-2', credentials:'jenkins-aws') {
					sh '''
						eksctl create cluster \
						--name capstonegreencluster \						
						--nodegroup-name standard-workers \
						--node-type t2.small \
						--nodes 1 \
						--nodes-min 1 \
						--nodes-max 3 \						
					'''
				}
			}
		}

		stage('create greencluster kubectl config') {
			steps {
				withAWS(region:'us-east-2', credentials:'jenkins-aws') {
					sh '''
						aws eks --region us-east-2 update-kubeconfig --name capstonegreencluster
					'''
				}
			}
		}

	}
}
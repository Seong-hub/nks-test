pipeline {
	agent any
	stages {
		stage("Get Source") {
			steps {
				git branch: 'main', url: 'https://github.com/Seong-hub/nks-test.git'
			}
	        }


	stage("Build Microservice image") {
		steps {                 
			script {
				try {
				appImage = docker.build("lalll5555/nks-test")
				} catch (e) {sh "echo docker build fail"}
				docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-ID') {
					try {
				               appImage.push("${env.BUILD_NUMBER}")
				                      appImage.push("latest")
					} catch (e) { sh 'echo docker push fail'}
				}
            		}                                                 
        	}
	}
//        stage("Deploy to Kubernetes") {
//            steps {
//                sh 'curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl'
//                sh 'chmod +x ./kubectl'
//                sh 'kubectl apply -f ./deployment.yaml --kubeconfig=/root/kubeconfig.yaml'
//            }
//        }

        stage("Deployment list check") {
            steps {
//               sh "kubectl get deployments.apps -A --kubeconfig=/root/kubeconfig.yaml"
		sh "hostname -f"
		sh "kubectl get nodes"
            }
        }
}
}

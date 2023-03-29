pipeline {
	agent any
	stages {
		stage("Get Source") {
			steps {
				git branch: 'main', url: 'https://github.com/Seong-hub/nks-test.git'
			}
	        }


//	stage("Build Microservice image") {
//		steps {                 
//			script {
//				try {
//				appImage = docker.build("lalll5555/nks-test")
//				} catch (e) {sh "echo docker build fail"}
//				docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-ID') {
//					try {
//				               appImage.push("${env.BUILD_NUMBER}")
//				                      appImage.push("latest")
//					} catch (e) { sh 'echo docker push fail'}
//				}
//            		}                                                 
//        	}
//	}

	stage("Make ncp-iam-authenticator") {
		steps {
			sh "curl -o ncp-iam-authenticator -L https://github.com/NaverCloudPlatform/ncp-iam-authenticator/releases/latest/download/ncp-iam-authenticator_linux_amd64"
			sh "chmod +x ./ncp-iam-authenticator"
			sh "mkdir -p $HOME/bin && cp ./ncp-iam-authenticator $HOME/bin/ncp-iam-authenticator && export PATH=$PATH:$HOME/bin"
			sh "echo 'export PATH=$PATH:$HOME/bin' >> ~/.bash_profile"
			sh "$HOME/bin/ncp-iam-authenticator help"
		}
	}
//        stage("Deployment list check") {
//            steps {
//		sh "kubectl get deployments.apps -A"
//            }
//        }
}
}

pipeline {
	agent any
	stages {
		stage("Get Source") {
			steps {
				git branch: 'main', url: 'https://github.com/Seong-hub/nks-test.git'
			}
	        }


	stage("Build && PUSH Microservice image") {
		// Credential 연동
	        environment {
			nks_cr_cred = credentials('nks-cr-ID')
		}
	}
	stage("Build Microservice image") {
		steps {                 
			script {
				try {
				appImage = docker.build("lalll5555/nks-test")
				} catch (e) {sh "echo ########################docker build fail#################################"}
					docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-ID') {
					try {
				               appImage.push("${env.BUILD_NUMBER}")
			                       appImage.push("latest")
					} catch (e) { sh 'echo ###########################docker push fail###############################'}
					}
                	      	}
		}                                                                                
        }
      	
//		steps {                 
//			script {
//				try {
//				appImage = docker.build("lsb-nks-test-cr.kr.ncr.ntruss.com/nks-test:'${env.BUILD_NUMBER}'")
//				appImage = docker.build("lalll5555/nks-test'")
//				} catch (e) {sh "echo ####################docker build fail#######################"}
//				sh "docker login -u '$nks_cr_cred_USR' -p '$nks_cr_cred_PSW' lsb-nks-test-cr.kr.ncr.ntruss.com"
//				sh "docker push lalll5555/nks-test:'${env.BUILD_NUMBER}'"
//				sh "docker push lsb-nks-test-cr.kr.ncr.ntruss.com/nks-test:'${env.BUILD_NUMBER}'"
//				sh "docker push lsb-nks-test-cr.kr.ncr.ntruss.com/nks-test:latest"
//				}
//			}
//	}                                                 

//	stage("Make ncp-iam-authenticator") {
//		steps {
//			sh "curl -o ncp-iam-authenticator -L https://github.com/NaverCloudPlatform/ncp-iam-authenticator/releases/latest/download/ncp-iam-authenticator_linux_amd64"
//			sh "chmod +x ./ncp-iam-authenticator"
//			sh "mkdir -p $HOME/bin && cp ./ncp-iam-authenticator $HOME/bin/ncp-iam-authenticator && export PATH=$PATH:$HOME/bin"
//			sh "echo 'export PATH=$PATH:$HOME/bin' >> ~/.bash_profile"
//			sh "ncp-iam-authenticator help"
//		}
//	}
//        stage("Deployment list check") {
//            steps {
//		sh "kubectl get deployments.apps -A"
//            }
//        }
}
}

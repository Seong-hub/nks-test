pipeline {
	agent any {
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
	stage( "depolyment list check" ) {
		steps {
			sh "kubectl get deployments.apps -A"
		}       
	}
}
}
}

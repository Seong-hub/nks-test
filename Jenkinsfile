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
	        environment { nks_cr_cred = credentials('nks-cr-ID') }
                steps {
                        script {
                                try {
				appImage = docker.build("lsb-nks-test-cr.kr.ncr.ntruss.com/nks-test")
                                } catch (e) {sh "echo ########################docker build fail#################################"}
                                sh "docker login -u '$nks_cr_cred_USR' -p '$nks_cr_cred_PSW' lsb-nks-test-cr.kr.ncr.ntruss.com"
                                        try {
                                               appImage.push("lsb-nks-test-cr.kr.ncr.ntruss.com/nks-test:'${env.BUILD_NUMBER}'")
                                               appImage.push("latest")
                                        } catch (e) { sh 'echo ###########################docker push fail###############################'}
                                }
                }
	}
}
}

def gv

pipeline {
	
	agent any
	
	stages {
		stage("init") {
			steps {
				script {
					gv = load("script.groovy")
				}
			}
		}
		
		stage("package") {
			steps {
				script {
					gv.packageApp()
				}
			}
		}
	}
	post {
		success {
			deploy adapters: [tomcat8(credentialsId: 'f4ea2c60-5173-4000-9f34-950c44fb4c03', path: '', url: 'http://192.168.1.10:8090/')], contextPath: 'chandu', war: '**/*.war'
		}
		failure {
			//Mail must send to respective person if build fails...
			mail bcc: '', body: 'Sorry...Your Build is failed....', cc: '', from: '', replyTo: '', subject: 'Build Failure', to: 'sekharchandra2108@gmail.com'
		}
	}
}

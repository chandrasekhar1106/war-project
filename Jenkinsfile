def gv

pipeline {
	
	agent any
	
	tools {
		maven 'Maven'
	}
	
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
			mail bcc: '', body: 'Sorry....Your pipeline failed...', cc: '', from: 'chandraganimisetty@gmail.com', replyTo: 'sekharchandra2108@gmail.com', subject: 'Pipeline Failed ', to: 'sekharchandra2108@gmail.com'
		}
	}
}

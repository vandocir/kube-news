pipeline{
	agent any

	stages{
		
		stage("Build Docker Image"){
			steps {
				script{
					dockerapp = docker.build("vandocir/kube-news:${env.BUIL_ID}","-f ./src/Dockerfile ./src")
				}
			}
		}
	}
}
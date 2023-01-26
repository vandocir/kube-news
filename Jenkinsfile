pipeline{
	agent any

	stages{
		
		stage("Build Docker Image"){
			steps {
				script{
					dockerapp = docker.build("vandocir/kube-news:${env.BUILD_ID}","-f ./src/Dockerfile ./src")
				}
			}
		}

		stage("Push Docker Image"){
			steps {
				script{
					docker.withRegistry("https://registry.hub.docker.com","dockerhub") {
						dockerapp.push("latest")
						dockerapp.push("${env.BUILD_ID}")
					}
				}
			}
		}

		stage("Deploy Kubernates"){
			steps {
				withKubeConfig([credentialsId: 'kubeconfig']) {
					sh 'kubectl apply -f ./src/k8s/deployment.yaml'		
				}
			}
		}
	}
}
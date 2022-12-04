node {
	def application = "springbootapp"
	def dockerhubaccountid = "Harsha441"
	stage('Clone repository') {
		checkout scm
	}

	stage('Build image') {
		app = docker.build("${dockerhubaccountid}/${application}:${BUILD_NUMBER}")
	}

	stage('Push image') {
		withDockerRegistry([ credentialsId: "Harsha441", url: "https://hub.docker.com/u/harsha441" ]) {
		app.push()
		app.push("latest")
	}
	}

	stage('Deploy') {
		sh ("docker run -d -p 81:8080 -v /var/log/:/var/log/ ${dockerhubaccountid}/${application}:${BUILD_NUMBER}")
	}
	
	stage('Remove old images') {
		// remove docker pld images
		sh("docker rmi ${dockerhubaccountid}/${application}:latest -f")
   }
}

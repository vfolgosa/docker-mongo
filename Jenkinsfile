node {
	docker.withRegistry('http://54.233.110.154:5043', 'docker-repository-credentials') {
		def app

		stage('Clone repository') {
			checkout scm
		}

		stage('Build image') {
			
				app = docker.build("b2w/mongo")
			
		}

		stage('Test image') {
			app.inside {
				sh 'echo "Tests passed"'
			}
		}

		stage('Push image') {
			
				app.push("${env.BUILD_NUMBER}")
				app.push("latest")
			
		}
		
		stage('Run image') {
			
				app.run('-p 27017:27017')
			
		}
	}
}
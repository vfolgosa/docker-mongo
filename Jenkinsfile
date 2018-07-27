node {

	def customImage
	
	stage('Clone repository') {
		checkout scm
    }
    
	docker.withRegistry('http://54.233.110.154:5043', 'docker-repository-credentials') {
		stage('Build image') {
			customImage = docker.build("planets-mongodb")
		}
        stage('Push image') {
			customImage.push("${env.BUILD_NUMBER}")
            customImage.push("latest")
			
		}
		stage('Stopping previus container') {
			sh 'docker stop planets-mongodb'			
		}
		stage('Run image') {
			customImage.run('-p 27017:27017')
		}
    }
	
	
}

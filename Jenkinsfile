node {

	def customImage
	
	stage('Clone repository') {
		checkout scm
    }
    
	docker.withRegistry('http://54.233.110.154:5043', 'docker-repository-credentials') {
		stage('Build image') {
			customImage = docker.build("mongo:${env.BUILD_ID}")
		}
        stage('Push image') {
			customImage.push()
		}
		stage('Run image') {
			customImage.run('-p 27017:27017')
		}
    }
	
	
}

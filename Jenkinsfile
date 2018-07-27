node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Build image') {
		app = docker.build("getintodevops/hellonode")
    }

    stage('Test image') {
        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        docker.withRegistry('http://54.233.110.154:5043', 'docker-repository-credentials') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
	
	stage('Run image') {
		docker.withRegistry('http://54.233.110.154:5043', 'docker-repository-credentials') {
			app.run('-p 27017:27017')
		}
	}
}
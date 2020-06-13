pipeline {
     agent any
     stages {
         stage('Build') {
             steps {
                 sh 'echo "Hello World"'
                 sh '''
                     echo "Multiline shell steps works too"
                     ls -lah
                 '''
             }
         }
		 
         stage('Lint HTML') {
              steps {
                  sh 'tidy -q -e *.html'
              }
         }
		 
		 stage('Building Docker image') {
			  steps {
				sh 'docker build -t static-nginx .'
			  }
		  }
			  
		 stage('Push Container') {
			  steps {
			      script {
				    docker.withRegistry('https://index.docker.io/v1', 'DockerHub') {
					  def image = docker.build('sivdoc/static-nginx:latest')
					  image.push()
					}
				  }
			  }
		 }

		 stage('Deploy container') {

				kubectl apply -f rolling-deploy.yaml
				kubectl apply -f service.yaml

		 }
	 }
}
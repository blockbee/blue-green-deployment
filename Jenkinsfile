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
				sh 'docker build -t static-container .'
			  }
			  
		 stage('Push Container') {
			  steps {
			      script {
				    docker.withRegistry('https://index.docker.io/v1', 'Dockerhub') {
					  def image = docker.build('sivdoc/static-container:latest')
					  image.push()
					}
				  }
			  }
		 } 
		 
	}
}
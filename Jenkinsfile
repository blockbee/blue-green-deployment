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

		 stage('Deploy container') {
			steps {
				sh 'kubectl apply -f rolling-deploy.yaml'
				sh 'kubectl apply -f service.yaml'
			}
		 }
	 }
}
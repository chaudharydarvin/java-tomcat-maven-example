pipeline {
    agent any
    stages {
    	stage('Code build') {
    	    steps {
    	        sh "mvn package"
    	    }
    	         	
    	}
    	stage('Docker build') {
    	    steps {
    	        sh '''
                try {               
                docker stop testcontainer
                docker rm $(docker ps -a -q)
                docker rmi $(docker images -a -q | grep -v "ubuntu")
                } catch(Exception error) {
                echo "ERROR DETECTED"
                error.getMessage()
                }
                docker build -t testimage .
                '''
    	    }
    	    
   	    }
    	stage('Smoke testing and result') {
    	    steps {
    	        echo "smoke testing"
    	    }
        
    	}
    	stage('Docker Start') {
    	    steps {
    	        sh '''
    	        docker run -d --name testcontainer -p 9000:8080 testimage
    	        '''
    	    }
    	}
    }
  }

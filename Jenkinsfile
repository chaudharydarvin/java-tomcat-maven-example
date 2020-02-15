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
                docker stop testcontainer &> /dev/null
                docker rm $(docker ps -a -q)
                docker rmi $(docker images -a -q | grep -v "ubuntu") &> /dev/null
                docker build -t testimage .
                '''
    	    }
    	    
   	    }
    	stage('Smoke testing and result') {
    	    steps {
    	        echo "smoke testing"
    	    }
        
    	}
    	stage('Docker build and start') {
    	    steps {
    	        sh '''
    	        docker run -d --name testcontainer -p 9000:8080 testimage
    	        '''
    	    }
    	}
    }
  }

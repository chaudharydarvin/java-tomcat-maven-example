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
    	        docker stop testcontainer 2> /dev/null
                docker rm $(docker ps -a -q) 2> /dev/null
                docker rmi $(docker images -a -q | grep -v "ubuntu") 2> /dev/null
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

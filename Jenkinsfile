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
                docker rm $(docker ps -q -a) &> /dev/null
                docker rmi $(docker images -a -q | grep -v "ubuntu") &> /dev/null
                sleep 10s
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
                sleep 10s
    	        docker run -d --name testcontainer -p 9000:8080 testimage
    	        '''
    	    }
    	}
    }
  }

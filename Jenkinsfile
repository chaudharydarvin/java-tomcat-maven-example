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
                sleep 10s
                docker rm $(docker ps -q -a) &> /dev/null
                sleep 10s
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
                docker run -d --name testcontainer -p 9000:8080 testimage
    	        '''
    	    }
    	}
    }
  }

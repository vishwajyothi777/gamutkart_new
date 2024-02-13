pipeline {
    agent any

//	tools {
//		jdk 'jdk8'
//	}
//	environment {
//		M2_INSTALL = "/usr/bin/mvn"
//	}

    stages {
        stage('Clone-Repo') {
	    	steps {
	        	checkout scm
	    	}
        }
	    
	stage('Compile') {
            steps {
                sh 'mvn install compile'
            }
        }
	    
        stage('Build') {
            steps {
                sh 'mvn install -Dmaven.test.skip=true'
            }
        }
		
        stage('Unit Tests') {
            steps {
                sh 'mvn compiler:testCompile'
                sh 'mvn surefire:test'
                junit 'target/**/*.xml'
            }
        }
	    
	stage('Package as war') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Deployment') {
            steps {
                sh 'sshpass -p staragile scp target/gamutkart.war staragile@172.31.93.157:/home/staragile/apache-tomcat-9.0.85/webapps'
            }
        }
    }
}

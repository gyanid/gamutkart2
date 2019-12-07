pipeline {
    agent any

	tools {
		maven 'maven3.6'
	}
//
//	environment {
//		M2_INSTALL = "/home/gamut/Distros/apache-maven-3.6.0/bin/mvn"
//	}

    stages {
		stage('Clone-Repo') {
			steps {
				checkout scm
			}
		}
		stage('Build') {
	    	steps {
				sh 'mvn install -DskipTests'
			}
	    }
		stage('Unit Tests') {
			steps {
				sh 'mvn surefire:test'
			}
		}
		stage('Deployment') {
	    	steps {
				sh 'sshpass -p "gyan@123" scp target/gamutkart.war ttomcat@172.17.0.3:/home/ttmocat/software/apache-tomcat-8.5.45/webapps'
				sh 'sshpass -p "gyan@123" ssh ttomcat@172.17.0.3 "JAVA_HOME=/home/jjenkin/software/jdk1.8.0_181" "/home/jjenkin/software/apache-tomcat-8.5.45/bin/startup.sh"'
	    	}
		}
    }
}

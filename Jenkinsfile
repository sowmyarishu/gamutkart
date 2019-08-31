pipeline {
    agent any

	tools {
		maven 'maven3.6'
	}

//	environment {
//		M2_INSTALL = "/home/sandeep/distore/apache-maven-3.6.1/bin/mvn"
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
				sh 'sshpass -p "sandeep" scp target/gamutkart.war sandeep@172.17.0.2:/sarala/apache-tomcat-8.5.38/webapps'
				sh 'sshpass -p "sandeep" ssh sandeep@172.17.0.2 "JAVA_HOME=/sarala/jdk1.8.0_151" "/sarala/apache-tomcat-8.5.38/bin/startup.sh"'
	    	}
		}
    }
}

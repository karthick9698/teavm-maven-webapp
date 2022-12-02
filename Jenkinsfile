pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'github_cred', url: 'https://github.com/devopsdeepdive/teavm-maven-webapp.git']]])
            }
        }
	stage('Build') {
            steps {
                sh 'mvn compile'
            }
        }
	stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
	stage('Package') {
            steps {
                sh 'mvn package'
            }
        
	stage ('Deploy') {
            steps {
	     sshagent(['tomcat_deploy']) {
                sh 'scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/maven-deploy/target/teavm-maven-webapp-1.0-SNAPSHOT.war ubuntu@54.249.50.107:/opt/apache-tomcat-8.5.84/webapps'    
	     }
        }
	}
	}
    }

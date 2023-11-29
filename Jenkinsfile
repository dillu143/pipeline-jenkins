pipeline {
    agent any

    tools {
        maven "mvn"
    }

    stages {
        stage('code') {
            steps {
                git 'https://github.com/dillu143/JavaWebCalculator.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn package'
            }
        }
        stage('test') {
            steps {
            withSonarQubeEnv('sonar') {
           sh 'mvn sonar:sonar'
}
            }
        }
        stage('artificats') {
            steps {
  nexusArtifactUploader artifacts: [[artifactId: 'LoginWebApp', classifier: '', file: '/var/lib/jenkins/workspace/nexus -present/target/LoginWebApp.war', type: 'war']], credentialsId: '28-11', groupId: 'com.javawebtutor', nexusUrl: '3.93.218.40:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-releases', version: '1.0'
            }
        }
         stage('deploy') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'classsss', path: '', url: 'http://3.93.181.144:8089/')], contextPath: null, war: '**/*.war'
            }
        }
    }
}


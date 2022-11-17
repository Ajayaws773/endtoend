pipeline {
	agent any
	stages {
	stage('code') {
       steps {
          git changelog: false, poll: false, url: 'https://github.com/Ajayaws773/mavenrepo.git'
    
       }
     }
     stage('build') {
       steps {
          sh 'mvn package'
    
       }
     }
     stage('scan') {
       steps {
          sh '''mvn clean verify sonar:sonar \\
  -Dsonar.projectKey=test \\
  -Dsonar.host.url=http://3.111.40.104:9000 \\
  -Dsonar.login=sqp_0353ea697c303e711a33c9edd3c2ebf48c22d60d'''
       }
     }
     stage('artifact') {
       steps {
          nexusArtifactUploader artifacts: [
          [
          artifactId: 'studentapp', 
          classifier: '', 
          file: 'target/studentapp-2.5-SNAPSHOT.war', 
          type: 'war'
          ]
          ], 
          credentialsId: 'nexus3', 
          groupId: 'com.jdevs', 
          nexusUrl: '52.66.14.159:8081', 
          nexusVersion: 'nexus3', 
          protocol: 'http', 
          repository: 'maven-snapshots/', 
          version: '2.5-SNAPSHOT'
       }
     }
     stage('deploy') {
       steps {
          deploy adapters: [tomcat9(credentialsId: 'tomcatusr', path: '', url: 'http://65.0.5.251:8080/')], contextPath: null, war: '**/*.war'
       }
     }


     }
}

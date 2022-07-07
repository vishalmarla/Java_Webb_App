pipeline {
    agent any
    tools {
    maven 'maven3'    
    }

    stages {
        stage('sourcecode') {
            steps {
                git credentialsId: 'git', url: 'https://github.com/vishalmarla/Java_Webb_App.git'
            }
        }
         stage('compile') {
            steps {
               sh 'mvn clean compile' 
            }
        }
         stage('test') {
            steps {
               sh 'mvn clean test' 
            }
        }
       
       
        stage('sonar') {
            steps {
               withSonarQubeEnv('sonar') {
                  sh 'mvn clean package sonar:sonar'
                }
            
            }
        }
            
        stage('deploy') {
            steps {
                 deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://34.238.242.24:8090/')], contextPath: null, war: '**/*.war' 
            }
        }
              

        
    }
}




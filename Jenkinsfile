pipeline{
    agent any
    tools {
        maven 'maven-3.9.10'
    }
    stages{
        stage('clone'){
            steps{
                git 'https://github.com/lavanyavasudev/chatroom.git'
            }  
        }
        stage('validate'){
            steps{
                sh 'mvn --version'
                sh 'mvn clean validate'
            }
        }
        stage('compile'){
            steps{
                sh 'mvn compile'
            }
        }
        stage('trivy'){
            steps{
                sh 'trivy fs --format json --output trivy-fs-result.json .'
            }
        }
        stage('package'){
            steps{
                sh 'mvn package'
            }
        }
        stage('deploy'){
            steps{
                sh 'cp -r target/*.war /usr/local/tomcat/webapps/ROOT.war'
            }
        }
    }
}
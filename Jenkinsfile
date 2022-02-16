pipeline {
    agent any
    
    stages {
        stage('checkout'){
            steps{
                git branch: 'main', url: 'https://github.com/varrarajasekharbabu/project-work.git'
            }
        }
        stage('build'){
            steps{
                sh "mvn clean package"
            }
        }
        stage('SonarQube analysis') {
            steps{
                withSonarQubeEnv('sonarQube-8.9.6') {
                // withSonarQubeEnv {
                sh "mvn sonar:sonar"
                    
                }
                    
            }
        }
        stage('upload artifacts to nexus') {
            steps{
                nexusArtifactUploader artifacts: [[artifactId: 'WebApp', classifier: '', file: 'target/WebApp.war', type: 'war']], credentialsId: '7d904c95-eda1-4574-b8a0-ab9760f3c07a', groupId: 'lu.amazon.aws.demo', nexusUrl: 'localhost', nexusVersion: 'nexus3', protocol: 'http', repository: 'http://localhost:8081/repository/pipeline/', version: '1.0'
            }
        }
        stage('email notification') {
            steps{
                mail bcc: '', body: 'Build was successful', cc: '', from: '', replyTo: '', subject: 'test mail', to: 'sparameswarreddy321@gmail.com'
            }
        }
    }
}

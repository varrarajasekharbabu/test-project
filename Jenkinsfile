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
        stage('email notification') {
            steps{
                mail bcc: '', body: 'Build was successful', cc: '', from: '', replyTo: '', subject: 'test mail', to: 'sparameswarreddy321@gmail.com'
            }
        }
    }
}

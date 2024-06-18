pipeline{
    agent any
    stages{
        stage('zip the file'){
            steps{
                sh 'zip ansible-${BUILD_ID}.zip*--excule Jenkinsfile'
                sh 'ls -l'
            }
        }
        
    }
}
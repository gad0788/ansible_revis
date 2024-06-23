pipeline{
    agent any
    
    stages{
        stage('zip the files'){
            steps{
                sh 'zip ansible-${BUILD_ID}.zip * --exclude Jenkinsfile'
                sh 'pwd'
            }
        }
    }
}
pipeline{
    agent any
    stages{
        stage('zip the file'){
            steps{
                sh 'zip ansible-${BUILD_ID}.zip*--excule Jenkinsfile'
                sh 'ls -l'
            }
        }
        stage('upload artifacts'){
            steps{
                sh 'curl -uadmin:AP3yQAuEtNW52NMLC1yXozr4nbt -T ansible-${BUILD_ID}.zip \
                "http://18.204.20.152:8081/artifactory/ansible-repo/ansible-${BUILD_ID}.zip"'
            }
        }
    }
}
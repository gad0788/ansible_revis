pipeline{
    agent any
    stages{
        stage('zip the file'){
            steps{
                sh 'zip ansible-${BUILD_ID}.zip *--excule Jenkinsfile'
                sh 'ls -l'
            }
        }
        stage('uploading artifacts to jfrog'){
            steps{
                sh 'curl -uadmin:AP3yQAuEtNW52NMLC1yXozr4nbt -T ansible-${BUILD_ID}.zip \
                "http://ec2-35-174-200-32.compute-1.amazonaws.com:8081/artifactory/ansible-repo/ansible-${BUILD_ID}.zip"'
            }
        }
        stage('publish to ansible server'){
            steps{
                sh 'sshPublisher(publishers: [sshPublisherDesc(configName: 'ansibleServer', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'ls', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '/home/ec2-user', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'ansible-${BUILD_ID}.zip')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])'
            }
        }
        
    }
}
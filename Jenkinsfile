pipeline{
    agent any
    
    stages{
        stage('zip the files'){
            steps{
                sh 'rm -rf *.zip || echo ""'
                sh 'zip -r ansible-${BUILD_ID}.zip * --exclude Jenkinsfile'
            }
        }
        stage('upload artifacts to jfrog artifactory'){
            steps{
                sh 'curl -uadmin:AP3yQAuEtNW52NMLC1yXozr4nbt -T ansible-${BUILD_ID}.zip \
                "http://ec2-100-24-242-8.compute-1.amazonaws.com:8081/artifactory/ansible-repo/ansible-${BUILD_ID}.zip"'
            }
        }
        stage('publish to ansible server'){
            steps{
                sshPublisher(publishers: [sshPublisherDesc(configName: 'ansibleServer', transfers: [sshTransfer(cleanRemote: false, excludes: '', \
                execCommand: 'unzip -o ansible-${BUILD_ID}.zip;rm -rf ansible-${BUILD_ID}.zip', execTimeout: 120000, flatten: false, \
                makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', \
                remoteDirectory: '.', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'ansible-${BUILD_ID}.zip')], \
                usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
    }
}
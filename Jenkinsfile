pipeline{
    agent any

    stages{
        stage("zip the file"){
            steps{
                sh 'zip ansible-${BUILD_ID}.zip * --exclude Jenkinsfile || echo ""'
            }
        }
        stage("Upload artifact in JFrog"){
            steps{
                sh 'curl -uadmin:AP8gcgmmset5jeYChTJYDN6XmDd -T \
                ansible-${BUILD_ID}.zip "http://ec2-18-205-235-142.compute-1.amazonaws.com:8081/artifactory/ansible-dev/ansible-${BUILD_ID}.zip"'
            }
        }
        stage("Publish to ansible server"){
            steps{
                sshPublisher(publishers: [sshPublisherDesc(configName: 'ansible-server', \
                transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'ls', execTimeout: 120000, flatten: false, makeEmptyDirs: false, \
                noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '/home/ec2-user', remoteDirectorySDF: false, removePrefix: '', \
                sourceFiles: 'ansible-${BUILD_ID}.zip')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
    }
}
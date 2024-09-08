pipeline{
    agent any

    stages{
        stage("zip the file"){
            steps{
                sh 'zip -r ansible-${BUILD_ID}.zip --exclude Jenkinsfile || echo ""'
                sh 'ls -l'
            }
        }
    }
}
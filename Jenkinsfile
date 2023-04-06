pipeline {
    agent any

    tools { nodejs '19.8.1' }

    stages {
        stage('install') {
            steps{
            sh "npm install"
            }
        }

        stage('build dist') {
            steps{
            sh "npm run build"
            }
        }
        stage('artifacts to s3') {
            steps{
                withAWS(region:'ap-southeast-1',credentials:'s3user') {
                  sh 'echo "Uploading content with AWS creds"'
                      s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file:'test/dist/test/*', bucket:'angular-test-jenkins')
                  }  
            } 
        }
    }
}

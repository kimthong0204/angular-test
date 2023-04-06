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
            steps {
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding',
                accessKeyVariable: 'AKIA45LVDVLNR7T7ULH2',
                secretKeyVariable: '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',
                credentialsId: 's3user']]) {
                    sh "aws s3 ls"
                    sh "aws s3 mb s3://angular-test-jenkins"
                    sh "aws s3 cp test/dist/test/* s3://angular-test-jenkins"
                }
            } 
        }
    }
}

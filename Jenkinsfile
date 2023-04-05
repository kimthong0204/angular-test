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
            sh "ng build --configuration production --aot"
            }
        }
        stage('artifacts to s3') {
            steps {
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding',
                accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                secretKeyVariable: 'AWS_SECRET_ACCESS_KEY',
                credentialsId: 'AWS_ACCOUNT']]) {
                    sh "aws s3 ls"
                    sh "aws s3 mb s3://angular-test-jenkins"
                    sh "aws s3 cp test/dist/test/* s3://angular-test-jenkins"
                }
            } 
        }
    }
}

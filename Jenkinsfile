pipeline {
    agent any

    stages {
        stage('build dist') {
            steps{
            sh "ng build --configuration production --aot"
            }
        }
        stage('artifacts to s3') {
            try {
                withCredentials([<object of type com.cloudbees.jenkins.plugins.awscredentials.AmazonWebServicesCredentialsBinding>]) {
                    sh "aws s3 ls"
                    sh "aws s3 mb s3://angular-test-jenkins"
                    sh "aws s3 cp test/dist/test/* s3://angular-test-jenkins"
                }
            } catch (err) {
                sh "echo error is sending"
            }
        }
    }
}

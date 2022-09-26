pipeline {
    agent any
    withCredentials([[
        $class: 'AmazonWebServicesCredentialsBinding',
        credentialsId: "aws-rts",
        accessKeyVariable: 'AWS_ACCESS_KEY_ID',
        secretKeyVariable: 'AWS_SECRET_ACCESS_KEY'
    ]])
    stages {
        stage('Build') {
            steps {
                sh 'echo "Building"'
                sh 'echo $AWS_ACCESS_KEY_ID'
                sh 'echo $AWS_SECRET_ACCESS_KEY'
            }
        }
        stage('Test') {
            steps {
                sh 'echo "Testing"'
            }
        }
        stage('Publish') {
            steps {
                sh 'echo "Publishing"'
            }
            post {
                success {
                    sh 'echo "Deploying to EB"'
                    sh 'sudo chmod 775 ./deploy_app.sh'
                    sh './deploy_app.sh'
                }
            }
        }
    }
}
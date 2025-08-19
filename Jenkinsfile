pipeline {
    agent any
    environment {
        AWS_REGION = 'us-west-2' 
        ECR_REPO = 'my-test-repository'
    }
    stages {
        stage('Test ECR Access') {
            steps {
                script {
                    withAWS(credentials: 'AWScred', region: AWS_REGION) { 
                        sh "aws ecr create-repository --repository-name ${ECR_REPO}" 
                    }
                }
            }
        }
    }
}

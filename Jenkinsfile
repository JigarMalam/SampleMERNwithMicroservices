pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = "us-west-2"   
        ACCOUNT_ID = "975050024946"    
        IMAGE_TAG = "latest"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', credentialsId: 'JigarGit', url: 'https://github.com/JigarMalam/SampleMERNwithMicroservices.git'
            }
        }

        stage('Login to ECR') {
            steps {
                withAWS(credentials: 'AWScred', region: "${AWS_DEFAULT_REGION}") {
                    sh """
                      aws ecr get-login-password --region ${AWS_DEFAULT_REGION} \
                        | docker login --username AWS --password-stdin ${ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com
                    """
                }
            }
        }

        stage('Build & Push Docker Images') {
            steps {
                script {
                    def services = ["helloService-by-jigar", "profileService-by-jigar", "frontend-by-jigar"]
                    for (s in services) {
                        sh """
                          echo "Building image for ${s}"
                          docker build -t ${s}:$IMAGE_TAG ./${s}
                          docker tag ${s}:$IMAGE_TAG ${ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com/${s}:$IMAGE_TAG
                          docker push ${ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com/${s}:$IMAGE_TAG
                        """
                    }
                }
            }
        }
    }
}

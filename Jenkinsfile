pipeline {
    agent any
    options {
        // Timeout counter starts AFTER agent is allocated
        timeout(time: 60, unit: 'SECONDS')
    }
    stages {
        stage('ImageBuild') {
            steps {
                echo 'Building Image'
                docker build -t testapp:latest .
            }
        }
        stage('ECRPush') {
            steps {
                echo 'Pushing to ECR'
                aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 111111111111.dkr.ecr.ap-south-1.amazonaws.com
                docker tag testapp:latest 111111111111.dkr.ecr.ap-south-1.amazonaws.com/my-repository:latest
                docker push 111111111111.dkr.ecr.ap-south-1.amazonaws.com/my-repository:latest
            }
        }
    }
}

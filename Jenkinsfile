pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'docker build -t melong:latest .'
            }
        }

        stage('Login to ECR') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'Demo-ecs', usernameVariable: 'AWS_ACCESS_KEY_ID', passwordVariable: 'AWS_SECRET_ACCESS_KEY')]) {
                    sh 'eval $(aws ecr get-login --no-include-email --region eu-west-2)'
                }
            }
        }

        stage('Push to ECR') {
            steps {
                sh 'docker tag melong:latest 397783195241.dkr.ecr.eu-west-2.amazonaws.com/leparrain'
                sh 'docker push 397783195241.dkr.ecr.eu-west-2.amazonaws.com/leparrain'
            }
        }

        stage('Logout from ECR') {
            steps {
                sh 'docker logout 397783195241.dkr.ecr.eu-west-2.amazonaws.com/leparrain'
            }
        }
    }
}

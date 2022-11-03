pipeline {
    agent any

    stages {
        stage('AWS STS') {
            steps {
                echo 'AWS STS'
                sh 'aws sts get-caller-identity'
            }
        }
        stage('AWS S3 listar') {
            steps {
                sh 'aws s3 ls'
            }
        }
        stage('Git Clone') {
            steps {
                sh 'rm -rf S3-jenkins-web/'
                sh 'git clone https://github.com/Luxcrift/S3-jenkins-web.git'
                sh 'ls -lrt S3-jenkins-web/'
            }
        }
         stage('Upload to S3') {
            steps {
                sh 'aws s3 cp S3-jenkins-web s3://jenkins-mieulet --recursive'
            }
        }
    }
}

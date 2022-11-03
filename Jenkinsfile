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
                sh 'rm -rf desafio3-despliegue2/'
                sh 'git clone https://github.com/Luxcrift/desafio3-despliegue2.git'
                sh 'ls -lrt desafio3-despliegue2/'
            }
        }
         stage('Upload to S3') {
            steps {
                sh 'aws s3 cp desafio3-despliegue2 s3://desafio3-mieulet --recursive'
            }
        }
    }
}

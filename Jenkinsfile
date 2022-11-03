pipeline {
    agent any
    environment{
        FUNCTION_NAME="csvtoDynamoDBimport"
        BUCKETS3="desafio3-bucket"
        ZIP="data.zip"
        FILE="data.csv"
    }

    stages {
        stage('INIT') {
            steps {
                echo "Initializing Pipeline"
                sh 'aws sts get-caller-identity'
            }
        }
        stage('AWS S3 ls') {
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
        stage('BUILD TO ZIP') {
            steps {
                echo "Building Main"
                sh 'zip -jr $ZIP $FILE'
                sh 'ls -lrt'
            }
        } 
        stage('Upload to S3') {
            steps {
                sh 'aws s3 cp $ZIP s3://${BUCKETS3} --recursive'
            }
        } 
        stage('Deploy to Lambda') {
            steps {
                sh 'aws lambda update-function-code --function-name $FUNCTION_NAME --s3-bucket ${BUCKETS3} --s3-key $ZIP --publish'
            }
        }   
    }
}

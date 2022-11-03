pipeline {
    agent any
    environment{
        FUNCTION_NAME="csvtoDynamoDBimport"
        BUCKETS3="desafio3-bucket"
        ZIP="function.zip"
        CODE="lambda_function.py"
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
        stage('BUILD TO ZIP') {
            steps {
                echo "Building ${BRANCH_NAME}"
                sh 'zip -jr $ZIP $CODE'
                sh 'ls -lrt'
            }
        } 
        stage('Upload to S3') {
            steps {
                sh 'aws s3 cp $ZIP s3://${BUCKETS3}'
            }
        } 
        stage('Deploy to Lambda') {
            steps {
                sh 'aws lambda update-function-code --function-name $FUNCTION_NAME --s3-bucket ${BUCKETS3} --s3-key $ZIP --publish'
            }
        }   
    }
}

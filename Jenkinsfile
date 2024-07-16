pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'ap-south-1'
    }

    stages {
        stage('Prepare') {
            steps {
                echo 'Preparing...'
            }
        }

        stage('Build') {
            steps {
                echo 'Building...'
            }
        }

        stage('Upload to S3') {
            steps {
                script {
                    echo 'Checking if logo.png exists...'
                    bat 'if exist logo.png (echo File exists) else (echo File does not exist)'

                    echo 'Listing files in current directory:'
                    bat 'dir'
                  
                    withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 's3Test']]) {
                        echo 'Uploading to S3...'
                        bat 'aws s3 cp logo.png s3://jenkins-bucket-98741 /'
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
        }
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}

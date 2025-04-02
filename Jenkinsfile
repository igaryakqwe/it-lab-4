pipeline {
    agent any

    environment {
        BUILD_DIR = 'build'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/igaryakqwe/it-lab-4', credentialsId: 'github_jenkins_key'
            }
        }

        stage('Build') {
            steps {
                bat 'cmake -S . -B %BUILD_DIR%'  
                bat 'cmake --build %BUILD_DIR%'
            }
        }

        stage('Test') {
            steps {
                bat '.\\%BUILD_DIR%\\Debug\\vs_mkr_test1 --gtest_output=xml:report.xml'
            }
            post {
                always {
                    junit 'report.xml'
                }
            }
        }
    }

    post {
        success {
            echo 'Build and tests were successful!'
        }
        failure {
            echo 'Something went wrong!'
        }
    }
}
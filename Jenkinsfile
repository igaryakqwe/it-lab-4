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
                // Крок для збірки проекту з Visual Studio
                // Встановіть правильні шляхи до рішення/проекту та параметри MSBuild
                bat '"C:\\Program Files (x86)\\Microsoft Visual Studio\\2019\\BuildTools\\MSBuild\\Current\\Bin\\MSBuild.exe" test_repos.sln /t:Build /p:Configuration=Release'            }
        }

        stage('Test') {
            steps {
                // Команди для запуску тестів
                bat '.\\x64\\Debug\\test_repos.exe --gtest_output=xml:test_report.xml'            }
        }
    }

    post {
        always {
            junit 'test_report.xml'
        }
    }
}
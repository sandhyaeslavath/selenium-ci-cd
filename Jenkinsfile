pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning repository...'
                git branch: 'main', url: 'https://github.com/sandhyaeslavath/selenium-ci-cd.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project using Maven...'
                bat 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                echo 'Running Selenium tests...'
                bat 'mvn test'
            }
        }
    }

    post {
        always {
            echo 'Checking for test results...'
            script {
                if (fileExists('target/surefire-reports')) {
                    echo 'Publishing test reports...'
                    junit 'target/surefire-reports/*.xml'
                } else {
                    echo '⚠️ No test reports found, skipping test publishing.'
                }
            }
        }

        success {
            echo '✅ Build completed successfully!'
        }

        failure {
            echo '❌ Build failed. Please check the logs.'
        }
    }
}

pipeline {
    agent any

    tools {
        // Ensure you configured these in "Manage Jenkins → Tools"
        jdk 'Java17'
        maven 'Maven3'
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Cloning the GitHub repository...'
                git url: 'https://github.com/sandhyaeslavath/selenium-ci-cd.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project using Maven...'
                bat 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                echo 'Running Selenium test cases...'
                bat 'mvn test'
            }
        }

        stage('Package') {
            steps {
                echo 'Packaging the application...'
                bat 'mvn package'
            }
        }
    }

    post {
        always {
            echo 'Publishing test results...'
            junit 'target/surefire-reports/*.xml'
        }
        success {
            echo 'Build succeeded!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}

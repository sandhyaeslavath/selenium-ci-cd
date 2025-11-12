pipeline {
    agent any

    tools {
        jdk 'Java17'       // Jenkins JDK installation name (configure under Manage Jenkins → Tools)
        maven 'Maven3'     // Jenkins Maven installation name
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning the GitHub repository...'
                git branch: 'main', url: 'https://github.com/<your-username>/selenium-ci-cd.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the Maven project...'
                bat 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                echo 'Running Selenium tests...'
                bat 'mvn test'
            }
        }

        stage('Package') {
            steps {
                echo 'Packaging the project...'
                bat 'mvn package'
            }
        }
    }

    post {
        always {
            echo 'Publishing test results...'
            junit '**/target/surefire-reports/*.xml'
        }
    }
}

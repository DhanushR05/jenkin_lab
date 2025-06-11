pipeline {
    agent any

    tools {
        // Use the correct tool names as configured in Jenkins
        maven 'maven'   // Name must match the Maven installation name configured in Jenkins
        jdk 'java' 
        git 'git'
    }

    environment {
        MAVEN_OPTS = "-Dmaven.test.failure.ignore=true"  // Option to ignore test failures
    }

    stages {
        stage('Checkout') {
            steps {
                // Correct repository URL for your project
                git branch: 'main', url: 'https://github.com/DhanushR05/jenkin_lab.git'  // Your correct repository URL
            }
        }

        stage('Build') {
            steps {
                // Build the project using Maven
                sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                // Run tests using Maven
                sh 'mvn test'
            }
        }

        stage('Archive Artifacts') {
            steps {
                // Archive the build artifacts (JAR files)
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }

    post {
        always {
            // Ensure that the test reports are being archived correctly
            junit '**/target/surefire-reports/*.xml'  // Adjust path to match your test reports
        }
    }
}


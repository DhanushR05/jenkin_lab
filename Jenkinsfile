pipeline {
    agent any

    tools {
        maven 'maven'   // Ensure this matches the name of your Maven tool
        jdk 'java'      // Ensure this matches the name of your JDK tool
        git 'git'        // Ensure this matches the Git tool name configured in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the repository from GitHub
                git branch: 'main', url: 'https://github.com/DhanushR05/jenkin_lab.git'
            }
        }

        stage('Build') {
            steps {
                // Check if pom.xml exists in the current directory or adjust the directory if necessary
                script {
                    if (fileExists('pom.xml')) {
                        sh 'mvn clean install'
                    } else {
                        echo "pom.xml not found, skipping build"
                    }
                }
            }
        }

        stage('Test') {
            steps {
                // Example Maven test step
                sh 'mvn test'
            }
        }

        stage('Archive Artifacts') {
            steps {
                // Archive the artifacts generated by the build
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }

    post {
        always {
            junit '**/target/test-*.xml' // Specify the path to test results (if any)
        }
    }
}

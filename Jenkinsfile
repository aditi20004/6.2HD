pipeline {
    agent any

    tools {
        // Specify Maven and JDK versions configured in Jenkins' Global Tool Configuration
        maven 'Maven'
        jdk 'jdk-17'
    }

    environment {
        // Define environment variables
        JAVA_HOME = "${tool 'jdk-17'}"
    }

    stages {
        stage('Initialize') {
            steps {
                script {
                    // Cleanup workspace before starting a new build
                    deleteDir()
                }
            }
        }

        stage('Checkout') {
            steps {
                // Check out the code from the Git repository
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Compile the code and package it using Maven
                bat 'mvn clean package'
            }
            post {
                success {
                    echo 'Build succeeded.'
                }
                failure {
                    echo 'Build failed.'
                }
            }
        }

        stage('Test') {
            steps {
                // Run unit tests using Maven
                bat 'mvn test'
            }
            post {
                always {
                    // Collect test results for display in Jenkins UI
                    junit '**/target/surefire-reports/TEST-*.xml'
                }
                success {
                    echo 'Tests succeeded.'
                }
                failure {
                    echo 'Tests failed.'
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                // Here you would add commands to deploy your application
                // For example, deploying a .war file to a server
                // bat 'copy /Y path\\to\\your\\application.war path\\to\\deployment\\location'
            }
        }

        stage('Cleanup') {
            steps {
                // Perform cleanup if needed
                echo 'Cleaning up...'
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution complete.'
        }
    }
}

pipeline {
    agent any

    tools {
        // Specify the tools to auto-install and put on the PATH.
        maven 'Maven' // Replace with your version of Maven
        jdk 'jdk-17' // Replace with your JDK version
    }

    environment {
        // Define environment variables here.
        JAVA_HOME = "${tool 'jdk-17'}"
    }

    stages {
        stage('Initialize') {
            steps {
                // Clean the workspace before starting the build
                script {
                    // This is useful when your project requires a clean environment before building
                    deleteDir()
                }
            }
        }

        stage('Checkout') {
            steps {
                // Check out source code from a GitHub repository
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Run the Maven build command
                sh 'mvn clean package'
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
                // Run tests using Maven
                sh 'mvn test'
            }
            post {
                always {
                    // Archive the test results for Jenkins to display
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
            // This example assumes you might deploy to a staging environment
            steps {
                echo 'Deploying application...'
                // Add deployment scripts here, such as running scripts to deploy to servers or containers
                sh './deploy.sh' // This is a placeholder; replace with your actual deployment script
            }
        }

        stage('Cleanup') {
            steps {
                // Cleanup tasks if necessary
                echo 'Cleaning up post build and deployment...'
            }
        }
    }

    post {
        always {
            // Actions to take in all pipeline runs, like sending notifications or cleaning up
            echo 'Pipeline execution complete.'
        }
    }
}

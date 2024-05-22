pipeline {
    agent any

    tools {
        maven 'Maven 3.6.3' // Replace with the name of your Maven installation in Jenkins Global Tool Configuration
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    // Clean the directory
                    try {
                        sh "rm -rf *"
                    } catch (Exception e) {
                        echo "Error cleaning directory: ${e}"
                        currentBuild.result = 'FAILURE'
                        error("Failed to clean the directory.")
                    }

                    // Checkout the Git repository
                    try {
                        sh "git clone https://github.com/simoks/java-maven.git"
                    } catch (Exception e) {
                        echo "Error cloning repository: ${e}"
                        currentBuild.result = 'FAILURE'
                        error("Failed to clone the repository.")
                    }
                }
            }
        }
        stage('Build') {
            steps {
                script {
                    def currentDir = pwd()
                    echo "Current directory: ${currentDir}"
                    
                    // Navigate to the directory containing the Maven project
                    dir('java-maven') {
                        try {
                            // Run Maven commands
                            sh "${tool 'Maven 3.6.3'}/bin/mvn clean test package" // Reference the Maven tool configured in Jenkins
                        } catch (Exception e) {
                            echo "Error running Maven commands: ${e}"
                            currentBuild.result = 'FAILURE'
                            error("Maven build failed.")
                        }

                        try {
                            sh "java -jar target/maven-0.0.1-SNAPSHOT.jar"
                        } catch (Exception e) {
                            echo "Error running JAR file: ${e}"
                            currentBuild.result = 'FAILURE'
                            error("Failed to run the JAR file.")
                        }
                    }
                }
            }
        }
    }
}

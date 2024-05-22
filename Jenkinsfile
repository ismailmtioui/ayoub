pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Clean the directory
                sh "rm -rf *"
                // Checkout the Git repository
                sh "git clone https://github.com/simoks/java-maven.git"
            }
        }
        stage('Build') {
            steps {
                // Run Maven commands within the specified directory
                script {
                    def currentDir = pwd()
                    echo "Current directory: ${currentDir}"
                    
                    // Navigate to the directory containing the Maven project
                    dir('java-maven') {
                        // Run Maven commands
                        sh 'mvn clean test package'
                        sh "java -jar target/maven-0.0.1-SNAPSHOT.jar"
                    }
                }
            }
        }
    }
}


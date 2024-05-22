pipeline {
    agent any

    tools {
        maven 'Maven 3.6.3' // Replace with the name of your Maven installation in Jenkins Global Tool Configuration
    }

    stages {
        stage('Clean Workspace') {
            steps {
                // Clean the workspace directory
                deleteDir()
            }
        }
        stage('Checkout') {
            steps {
                // Checkout the Git repository
                git 'https://github.com/simoks/java-maven.git'
            }
        }
        stage('Build') {
            steps {
                script {
                    // Navigate to the directory containing the Maven project
                    dir('maven') {
                        // Run Maven commands using the Maven tool configured in Jenkins
                        sh "${tool 'Maven 3.6.3'}/bin/mvn clean test package"
                    }
                }
            }
        }
        stage('Run JAR') {
            steps {
                script {
                    // Run the generated JAR file
                    sh "java -jar maven/target/maven-0.0.1-SNAPSHOT.jar"
                }
            }
        }
    }
}



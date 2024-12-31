pipeline {
    agent any

    tools {
        jdk 'jdk-17'        // Set the JDK version you want to use
        maven 'Maven-3.9.9'  // Set the Maven version you want to use
    }

    stages {
        stage('Checkout') {
            steps {
                // Clone the repository from GitHub
                git 'https://github.com/itsmeteja9/jacoboot.git'  // Replace with your repository URL
            }
        }

        stage('Build and Test') {
            steps {
                // Run Maven clean install to compile the code and run tests
                bat 'mvn clean install'
            }
        }

        stage('Publish Unit Test Results') {
            steps {
                // Publish the JUnit test results from the correct directory
                junit '**/target/surefire-reports/TEST-*.xml'  // Adjusted to the default surefire-reports location
            }
        }

        stage('Publish JaCoCo Coverage Report') {
            steps {
                // Publish the JaCoCo coverage report
                jacoco execPattern: '**/target/jacoco.exec', 
                        classPattern: '**/target/classes', 
                        sourcePattern: '**/src/main/java', 
                        exclusionPattern: '**/test/**'
            }
        }
    }

    post {
        always {
            // Clean the workspace after the build
            cleanWs()
        }
    }
}

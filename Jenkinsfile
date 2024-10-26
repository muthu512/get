pipeline {
    agent any
    tools {
        maven 'Maven 3.9.9' // Ensure this matches the Maven configuration in Jenkins
    }
    stages {
        stage('Checkout') {
            steps {
                // Cloning the Git repository
                git 'https://github.com/muthu512/hello.git'
            }
        }
        stage('Build') {
            steps {
                // Running Maven build to generate the JAR file
                bat 'mvn clean package'
            }
        }
        stage('Deploy') {
            steps {
                script {
                    // Define the source and target paths for the JAR file
                    def jarSource = "${WORKSPACE}\\target\\spring-boot-hello-world-main.jar"
                    def deployFolder = "C:\\Users\\Dell-Lap\\Downloads\\Newfolder1"
                    
                    // Creating the deployment folder if it doesn't exist
                    bat "mkdir ${deployFolder}"
                    
                    // Copying the JAR file to the target folder
                    bat "copy ${jarSource} ${deployFolder}"
                    
                    // Running the Spring Boot application from the specific folder on port 1010
                    bat "start java -jar ${deployFolder}\\spring-boot-hello-world-main.jar --server.port=1010"
                }
            }
        }
    }
}

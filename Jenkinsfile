pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // This will automatically clone the repository based on the SCM configuration in Jenkins
                checkout scm
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                script {
                    def buildJar = "C:\\Users\\Dell-Lap\\.jenkins\\workspace\\DeploySpringBoot\\target\\spring-boot-2-hello-world-1.0.2-SNAPSHOT.jar"
                    def deployFolder = "C:\\Users\\Dell-Lap\\Downloads\\Newfolder"
                    def deployJar = "${deployFolder}\\spring-boot-2-hello-world-1.0.2-SNAPSHOT.jar"
                    bat "copy /Y \"${buildJar}\" \"${deployJar}\""
                    bat "java -jar \"${deployJar}\""
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed.'
        }
    }
}

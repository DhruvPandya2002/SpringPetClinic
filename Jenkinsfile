pipeline {
    agent any
    tools { maven 'm3' }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/DhruvPandya2002/SpringPetClinic.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn compile'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Package') {
            steps {
                sh 'mvn package'
                sh 'ls -l target'  // Display contents of the target directory to confirm JAR file location
            }
        }
        stage('Deploy') {
            steps {
                script {
                    def jarFile = '/var/lib/jenkins/workspace/PetClinicDedicatedPipeline/target/spring-petclinic-2.1.0.BUILD-SNAPSHOT.jar'
                    
                    // Check Java version
                    sh 'java -version'
                    
                    // Ensure the JAR file is executable
                    sh "chmod +x ${jarFile}"
                    
                    // Run the JAR file
                    sh "java -jar ${jarFile}"
                }
            }
        }
    }
}

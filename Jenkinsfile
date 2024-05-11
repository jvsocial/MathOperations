pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Check out your Maven project from Git
                git branch: 'master', url: 'https://github.com/jvsocial/MathOperations.git'
            }
        }
        
        stage('Build') {
            steps {
                // Run Maven compile
                sh 'mvn compile'
            }
        }
        
        stage('Unit Test') {
            steps {
                // Run Maven test
                sh 'mvn test'
            }
        }
        
        stage('Code Coverage') {
            steps {
                // Generate code coverage report using Jacoco
                sh 'mvn jacoco:report'
            }
            post {
                // Archive the code coverage report
                archiveArtifacts 'target/site/jacoco'
            }
        }
        
        stage('Package') {
            steps {
                // Build Maven package (e.g., JAR)
                sh 'mvn package'
            }
            post {
                // Archive the built artifact
                archiveArtifacts 'target/*.jar'
            }
        }
    }
}

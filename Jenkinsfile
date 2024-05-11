pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Check out your Maven project from Git
                git branch: 'demo-clover', url: 'https://github.com/jvsocial/MathOperations.git'
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
                // Run Clover instrumentation
                sh 'mvn clover:instrument'
                // Run Maven test again with Clover-instrumented code
                sh 'mvn test'
                // Generate Clover HTML report
                sh 'mvn clover:clover'
            }
            post {
                always {
                    // Archive the Clover HTML report
                    archiveArtifacts 'target/site/clover/*'
                }
            }
        }
        
        stage('Package') {
            steps {
                // Build Maven package (e.g., JAR)
                sh 'mvn package'
            }
            post {
                success {
                    // Archive the built artifact
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
    }
}

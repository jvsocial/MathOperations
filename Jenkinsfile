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
                always {
                    // Publish code coverage report using JacocoPublisher
                    step([$class: 'JacocoPublisher',
                        execPattern: 'target/*.exec',
                        classPattern: 'target/classes',
                        sourcePattern: 'src/main/java',
                        exclusionPattern: 'src/test*'
                    ])
                }
            }
        }
        
        stage('Package') {
            steps {
                // Build Maven package (e.g., JAR)
                sh 'mvn package'
            }
        }
    }
}

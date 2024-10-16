pipeline {
    agent any
    
    tools {
        maven 'maven 3.9.9' // Ensure this matches the Maven version configured in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                // Clone the Git repository for the current branch
                git branch: env.BRANCH_NAME, url: 'https://github.com/Nuvepro-Technologies-Pvt-Ltd/Devops_Jenkins_Maven_Proficient_Main.git'
            }
        }
        
        stage('Build') {
            steps {
                // Clean and build the Maven project
                sh 'mvn clean install'
            }
        }
        
        stage('Test') {
            steps {
                // Run the Maven tests
                sh 'mvn test'
            }
        }
        
        stage('Package') {
            steps {
                // Package the application
                sh 'mvn package'
            }
        }
    }

    post {
        success {
            // Archive the JAR and test results
            archiveArtifacts artifacts: 'target/*.jar', allowEmptyArchive: true
            junit '**/target/surefire-reports/*.xml'
        }
        always {
            // Clean up workspace after build
            cleanWs()
        }
    }
}

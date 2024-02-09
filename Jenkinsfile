pipeline {
    agent { label 'jenkins_Agent' }
    tools {
        jdk 'java17'
        maven 'Maven3'
    }
    stages {
        stage('Clean Up WorkSpace') {
            steps {
                cleanWs()
            }
        }

        stage('Clone the GitHub') {
            steps {
                echo 'Cloning GitHub repository...'
                git branch: 'main', credentialsId: 'Github_ID', url: 'https://github.com/sivaPrasad96/sample_devops_project.git'
            }
        }

        stage('Build the App') {
            steps {
                echo 'Building the application...'
                sh 'mvn clean package'
            }
        }

        stage('Test the App') {
            steps {
                echo 'Running tests...'
                sh 'mvn test'
            }
        }

        stage('SonarQube Analysis chk') {
            steps {
                echo 'Running SonarQube analysis...'
                script {
                    withSonarQubeEnv(credentialsId: 'jenkins_sonar_token') {
                        sh 'mvn sonar:sonar'
                    }
                }
            }
        }
    }
}
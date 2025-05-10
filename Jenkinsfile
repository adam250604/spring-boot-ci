pipeline {
    agent any

    environment {
        SONARQUBE = 'SonarQubeServer' // Replace with your SonarQube server name in Jenkins (Manage Jenkins > Configure)
        DOCKER_IMAGE = 'spring-boot-ci-image'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/adam250604/spring-boot-ci.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQubeServer') {
                    sh 'mvn sonar:sonar -Dsonar.projectKey=spring-boot-ci -Dsonar.host.url=http://localhost:9000'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t spring-boot-ci-image .'
            }
        }
    }

    post {
        success {
            echo '✅ CI/CD pipeline completed successfully!'
        }
        failure {
            echo '❌ CI/CD pipeline failed.'
        }
    }
}

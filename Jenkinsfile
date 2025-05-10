pipeline {
    agent any
    tools {
        maven 'Maven'   // Name of Maven tool in Jenkins
        jdk 'JDK17'     // Name of JDK tool in Jenkins
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', 
                url: 'https://github.com/adam250604/springbootcicd.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn sonar:sonar'
                }
            }
        }
        stage('Docker Build') {
            steps {
                script {
                    docker.build("adam250604/springboot-app:${env.BUILD_ID}")
                }
            }
        }
    }
}
pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS_ID = 'dockerhub-credentials'  // Must match the Jenkins credentials ID you created
        IMAGE_NAME = "madhu1520/nodejs-app"              // Replace with your DockerHub username and repo name
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/madhut115/nodejs-ci-cd-app'
            }
        }

       stage('Install Dependencies') {
           steps {
               bat 'npm install'
           }
       }

stage('Run Tests') {
    steps {
        bat 'npm test'
    }
}


        stage('Build Docker Image') {
            steps {
                bat 'docker build -t madhut115/nodejs-ci-cd-app .'
            }
        }


        stage('Push to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                bat 'docker login -u %DOCKER_USER% -p %DOCKER_PASS%'
                bat 'docker push madhut115/nodejs-ci-cd-app'
                }
            }
        }

    }


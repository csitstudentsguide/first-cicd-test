pipeline {
    agent any
    
    environment {
        DOCKERHUB_CREDENTIALS = credentials('subhashbhalerao-dockerhub')
    }

    stages {
        stage('Clone Code') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/csitstudentsguide/first-cicd-test.git']])
            }
        }
        
        stage('Build') {
            steps {
                sh 'docker build -t mywebapp .'
                sh 'docker image tag mywebapp subhashbhalerao/mywebapp'
            }
        }
        
        stage('Login') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        
        stage('Push') {
            steps {
                sh 'docker push subhashbhalerao/mywebapp'
            }
        }
    }

    post {
    always {
      sh 'docker logout'
    }
  }
}

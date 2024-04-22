pipeline {
    agent any

    environment {
        PATH = "/opt/sonar-scanner-4.6.2.2472-linux/bin:$PATH"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'assign01', 
                    url: 'https://github.com/AhmerKhan07/flask-project.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    withSonarQubeEnv('sonarcubeserver') {
                        sh '''
                        sonar-scanner \
                          -Dsonar.projectKey=python-scanner \
                          -Dsonar.sources=. \
                          -Dsonar.host.url=http://sonarqube:9000 \
                          -Dsonar.login=sqp_9b71c517ea496fc092f7b1ae6d93ccd21d850e1b
                        '''
                    }
                }
            }
        }

        stage('Build and Run Containers') {
            steps {
                script {
                    sh 'whoami'
                    sh 'sudo docker ps '
                    sh 'sudo docker-compose build appseed-app nginx'
                    sh 'sudo docker-compose up -d appseed-app nginx'
                }
            }
        }
    }
}

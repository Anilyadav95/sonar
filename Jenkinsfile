pipeline {
    agent any
    tools {
        maven 'Maven'
    }

    stages {
        stage('Git Checkout') {
            steps {
                checkout([$class: 'GitSCM',
                    branches: [[name: '*/main']],
                    extensions: [],
                    userRemoteConfigs: [[url: 'https://github.com/Anilyadav95/sonar']]
                ])
                echo 'Git Checkout Completed'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh '''
                        mvn clean verify sonar:sonar -Dsonar.projectKey=test-4 -Dsonar.projectName=test-4 -Dsonar.host.url=http://65.0.178.217:9000 -Dsonar.token=sqp_29b47710cf58ad55b04ecc3f2d91b7a10423bea2
           
                    '''
                    echo 'SonarQube Analysis Completed'
                }
            }
        }
    }
}

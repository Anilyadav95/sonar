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
                        mvn clean verify sonar:sonar -Dsonar.projectKey=test-2 -Dsonar.projectName=test-2 -Dsonar.host.url=http://65.0.178.217:9000 -Dsonar.token=sqp_bc0ed2630a3e42740e113bd16c6376250267f226
               
                    '''
                    echo 'SonarQube Analysis Completed'
                }
            }
        }
    }
}

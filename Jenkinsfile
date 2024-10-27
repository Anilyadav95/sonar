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
                        mvn clean verify sonar:sonar \
                        -Dsonar.projectKey=test \
                        -Dsonar.projectName=test \
                        -Dsonar.host.url=http://65.0.178.217:9000 \
                        -Dsonar.token=sqa_922704547ef74f922abc8f7aa74096d75c0e07ac
                    '''
                    echo 'SonarQube Analysis Completed'
                }
            }
        }
    }
}

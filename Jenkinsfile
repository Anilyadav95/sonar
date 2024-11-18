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
                        mvn clean verify sonar:sonar sonar-scanner -Dsonar.projectKey=latest -Dsonar.sources=. -Dsonar.host.url=http://43.204.215.226:9000 -Dsonar.token=sqp_a449b09198718e425e90406de284df93a7fa79a9
           
                    '''
                    echo 'SonarQube Analysis Completed'
                }
            }
        }
    }
}

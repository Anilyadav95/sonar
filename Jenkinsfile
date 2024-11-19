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
                        mvn clean verify 
                        sonar-scanner -Dsonar.projectKey=test -Dsonar.sources=. -Dsonar.host.url=http://52.66.84.14:9000 -Dsonar.token=sqp_900fddc6b97d78c0173c1cd4292d4513ea03adbe
           
                    '''
                    echo 'SonarQube Analysis Completed'
                }
            }
        }
    }
}

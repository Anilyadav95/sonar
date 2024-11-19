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
                        sonar-scanner -Dsonar.projectKey=testing19 -Dsonar.sources=. -Dsonar.host.url=http://52.66.84.14:9000 -Dsonar.token=sqp_9bafdc7b502a03bdab7db3f78d8964784ab95851406de284df93a7fa79a9
           
                    '''
                    echo 'SonarQube Analysis Completed'
                }
            }
        }
    }
}

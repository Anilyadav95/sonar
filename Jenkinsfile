pipeline {
    agent any
    tools {
        maven 'Maven'
    }

    environment {
        // Telegram credential IDs
        TELEGRAM_TOKEN = credentials('telegram-credentials')  // Ganti dengan ID kredensial Anda
        TELEGRAM_CHAT_ID = credentials('Telegram_ChatID')  // Ganti dengan ID kredensial Anda
    }

    stages {
        stage('Git Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/ZudaPradana/sonar']])
                echo 'Git Checkout Completed'
                echo "Token: ${TELEGRAM_TOKEN}"
                echo "Chat ID: ${TELEGRAM_CHAT_ID}"

            }
        }

        stage('SonarQube Analysis') {
            steps {
                // Tambahkan penundaan untuk memberikan waktu kepada server Spring Boot
                sleep time: 1, unit: 'MINUTES'
                withSonarQubeEnv('sq1') {
                    sh '''mvn clean verify sonar:sonar -Dsonar.projectKey=sonar-analysis -Dsonar.projectName='sonar-analysis' -Dsonar.host.url=http://localhost:9000'''
                    echo 'SonarQube Analysis Completed'
                }
            }
        }
    }

    post {
        always {
            script {
                def TEXT_MESSAGE = "Hello Zydd"
                sh "curl --location --request POST 'https://api.telegram.org/bot${TELEGRAM_TOKEN}/sendMessage' --form text='${TEXT_MESSAGE}' --form chat_id='${TELEGRAM_CHAT_ID}'"
            }
        }
    }
}

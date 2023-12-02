pipeline {
    agent any
    tools {
        maven 'Maven'
    }

    stages {
        stage('Git Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/ZudaPradana/sonar']])
                echo 'Git Checkout Completed'
            }
        }

        stage('Run Spring Report') {
            steps {
                script {
                    // Ganti perintah berikut dengan yang sesuai untuk menjalankan laporan Spring
                    sh 'mvn spring-report-plugin:run'
                }
            }
        }

        stage('SonarQube Analysis') {
            steps {
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
                // Notifikasi Telegram atau langkah-langkah lainnya
                buildNotify(
                    message: "Pipeline finished: ${currentBuild.result}",
                    recipient: "725260461",  // Ganti dengan username atau ID obrolan Telegram Anda
                    status: currentBuild.resultIsBetterOrEqualTo("SUCCESS") ? "SUCCESS" : "FAILURE"
                )
            }
        }
    }
}

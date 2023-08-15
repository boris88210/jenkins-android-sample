pipeline{
    agent any

    environment {
        IS_JENKINS = 'true'
        APP_VERSION = '1.0.0'
    }

    stages {
         stage('Build'){
             steps {
                sh './gradlew assembleDebug'
             }
         }
        stage('Parallel stage'){
            when {
                branch 'develop'
            }
            parallel {
                stage('Branch A') {
                    steps {
                        sh './gradlew assembleDebug'
                    }
                }
                stage('Branch B') {
                    steps {
                        sh './gradlew assembleDebug'
                    }
                }
            }
        }
        stage('UnitTest'){
             steps {
                sh './gradlew test'
             }
        }
        stage('Generate APK'){
                     steps {
                        sh './gradlew assembleDebug'
                     }
                 }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'app/build/outputs/**/*.apk', fingerprint: true
            }
        }
    }
}
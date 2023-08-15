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
                        echo "On Branch A, Build by Jenkins:"${IS_JENKINS}
                        echo "Version:"${APP_VERSION}
                    }
                }
                stage('Branch B') {
                    steps {
                         echo "On Branch A, Build by Jenkins: false"
                         echo "Version: 2.0.0"
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
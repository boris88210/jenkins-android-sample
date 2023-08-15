pipeline{
    agent any

    environment {
        IS_JENKINS = 'true'
        APP_VERSION = '1.0.0'
    }

    stages {
        stage('Build'){
             steps {
                sh './gradlew clean && rm -rf ./app/build/'
                sh './gradlew assembleDebug'
             }
        }
        stage('UnitTest'){
             steps {
                sh './gradlew test'
             }
        }
    }
}
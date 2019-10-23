pipeline {
    agent none
    stages {
        stage("build & SonarQube analysis") {
            agent any
            steps {
                withSonarQubeEnv('LocalSonarQube') {
                    sh 'mvn clean package sonar:sonar'
                }
            }
        }
        stage("Quality Gate") {
            steps {
                sleep(10)
                timeout(time: 3, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}
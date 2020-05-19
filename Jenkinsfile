pipeline {
        agent any
        stage('Sonarqube') {
             environment {
                scannerHome = tool 'SonarQubeScanner'
             }
             steps {
                withSonarQubeEnv('SonarQubeServer') {
                   sh "${scannerHome}/bin/sonar-scanner"
                }
                timeout(time: 10, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
             }
       }
}

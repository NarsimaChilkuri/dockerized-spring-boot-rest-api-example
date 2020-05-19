pipeline{
  agent any 
  stages{
    stage('SonarQube analysis') {
      environment {
        scannerHome = tool 'SonarQubeScanner'
      }
      steps {
          withSonarQubeEnv('SonarQubeScanner') {
            sh "${scannerHome}/bin/sonar-scanner"
          }
          timeout(time: 10, unit: 'MINUTES') {
            waitForQualityGate abortPipeline: true
          }
      }
    }
  }
}

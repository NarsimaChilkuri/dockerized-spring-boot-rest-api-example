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
          timeout(time: 1, unit: 'HOURS') {
              def qg = waitForQualityGate()
              if (qg.status != 'OK') {
                  error "Pipeline aborted due to quality gate failure: ${qg.status}"
              }
          }
      }
    }
  }
}

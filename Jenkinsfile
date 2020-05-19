pipeline {
        agent any
        stages {
             stage('Sonarqube') {
                 environment {
                     scannerHome = tool 'SonarQubeScanner'
                 }
                 steps {
                     withSonarQubeEnv('SonarQubeServer') {
                        sh "${scannerHome}/bin/sonar-scanner"
                     }
                     timeout(time: 1, unit: 'HOURS') {
                        steps{
                          def qg = waitForQualityGate()
                          if (qg.status != 'OK') {
                            error "Pipeline aborted due to quality gate failure: ${qg.status}"
                          }
                        }
                        
                     }
                 }
             }
        }

}

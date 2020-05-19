pipeline {
        agent any
        stages {
          stage("build & SonarQube analysis") {
            agent any
            steps {
              withSonarQubeEnv('SonarQubeScanner') {
                sh 'mvn clean package sonar:sonar'
              }
            }
          }
         stage("Quality Gate"){
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

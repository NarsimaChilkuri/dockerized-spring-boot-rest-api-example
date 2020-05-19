pipeline {
        agent any
        environment{
           DOCKER_TAG = getDockerTag() 
        }
        stages {
             stage('Sonarqube') {
                 environment {
                     scannerHome = tool 'SonarQubeScanner'
                 }
                 steps {
                     withSonarQubeEnv('SonarQubeServer') {
                        sh "${scannerHome}/bin/sonar-scanner"
                     }
                     timeout(time: 30, unit: 'MINUTES') {
                        script{
                          def qg = waitForQualityGate()
                          if (qg.status != 'OK') {
                            error "Pipeline aborted due to quality gate failure: ${qg.status}"
                          }
                          else{
                             steps{
                               withCredentials([usernamePassword(credentialsId: 'nexus-repo', passwordVariable: 'pass', usernameVariable: 'user')]) {
                                  sh "docker build . -t localhost:8081/repository/sonarqube-repo/spring-rest-api:${DOCKER_TAG}"
                                  sh "docker login localhost:8081 -u ${user} -p ${pass}"
                                  sh "docker push localhost:8081/repository/sonarqube-repo/spring-rest-api:${DOCKER_TAG}"
                               }
                             }

                          }
                        }
                        
                     }
                 }
             }
        }

}

def getDockerTag(){
  def tag = sh script: "git rev-parse HEAD", returnStdout: true
  return tag
}


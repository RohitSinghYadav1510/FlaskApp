pipeline {
   agent none
    options {
        skipStagesAfterUnstable()
       }
  stages {
     
     stage('Test Application') {
            agent {
                docker {
                    image 'rohit1015/flaskapp:v2'
                   }
                }
            steps {
              sh 'py.test --cov-report xml:coverage.xml --cov=. --junitxml=result.xml test.py'
              }
        }
    
     stage("Code Analysis Using Sonar"){
          agent any
          steps {
             sh 'docker run --rm --net=host -v ${PWD}:/sonarqube-flask sonarsource/sonar-scanner-cli sonar-scanner -D sonar.projectBaseDir=/sonarqube-flask'
            }
         }
     stage("Deploy"){
        agent any
        steps {
           sh 'kubectl get nodes'
        }
    }
}

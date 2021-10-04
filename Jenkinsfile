pipeline {
   agent none
    options {
        skipStagesAfterUnstable()
       }
     stages {
        
       stage('Build App'){
            agent any
          steps {
                sh '''
                docker build -t demo:v1 .
                docker images
                '''
            }
        }
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
    /*
     stage("Code Analysis Using Sonar"){
          agent any
          steps {
             sh 'docker run --rm --net=host -v ${PWD}:/sonarqube-flask sonarsource/sonar-scanner-cli sonar-scanner -D sonar.projectBaseDir=/sonarqube-flask'
            }
         }
     
     stage("Deploy"){
        agent any
        input{
                message "Do You Wanted To Deploy??"
            }
        steps {
           sh '''
           kubectl run myapp2 --image=rohit1015/flaskapp:v1
           kubectl expose pod myapp2 --port=5000 --type=LoadBalancer
           sleep 30
           kubectl get svc
           '''
        }
     }
     */
    }
}

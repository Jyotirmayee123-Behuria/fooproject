pipeline {
   agent any
  stages {
    stage('Checkout') {
       steps {
               git 'https://github.com/Jyotirmayee123-Behuria/fooproject.git/'
          }
     }
      stage ('Build') {
              steps {
                     bat "mvn compile"
                }
            }
           stage('Test') {
                steps {
                        bat "mvn test"
                     }
         post {
            always {
                  junit '**/target/surefire-reports/TEST*.xml'
              }
           }
        }
      }
    }
     

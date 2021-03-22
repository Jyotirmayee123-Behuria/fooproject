pipeline {
   agent any
  stages {
    stage('Checkout') {
       steps {
               git 'https://github.com/Jyotirmayee123-Behuria/fooproject/'
          }
     }
      stage ('Build') {
              steps {
                     sh "mvn compile"
                }
            }
           stage('Test') {
                steps {
                        sh "mvn test"
                     }
           stage('newman') {
                steps {
                        sh 'newman run Restful_Booker_Facit.postman_collection.json --environment Restful_Booker.postman_environment.json --reporters junit'
            }
            post {
                always {
                        junit '**/*xml'
                    }
                }
        }
         post {
            always {
                  junit '**/target/surefire-reports/TEST*.xml'
              }
           }
        }
      }
    }
     

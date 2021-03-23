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
           
            post {
            always {
                  junit '**/target/surefire-reports/TEST*.xml'
              }
           }
        }
		stage('newman') {
                steps {
                        sh 'newman run Restful_Booker.postman_environment1.json --environment Restful_Booker.postman_collection1.json --reporters junit'
            }
            post {
                always {
                        junit '**/*xml'
                    }
                }
        }
		
      }
    }
     
     

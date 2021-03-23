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
                sh 'newman run Restful_Booker.postman_collection1.json --environment Restful_Booker.postman_environment1.json --reporters junit'
            }
            post {
                always {
                        junit '**/*xml'
                    }
                }
        }

         stage('Robot') {
            steps {
                sh 'robot --variable BROWSER:headlesschrome -d Results Tests'
            }
            post {
                always {
                    script {
                        step(
                            [
                                $class                  :   'RobotPublisher',
                                outputPath              :   'Results',
                                outputFileName          :   '**/output.xml',
                                reportFileName          :   '**/report.html',
                                logFileName             :   '**/log.html',
                                disableArchiveOutput    :   false,
                                passThreshold           :   50,
                                unstableThreshold       :   40,
                                otherFiles              :   "**/*.png,**/*.jpg",
                            ]
                        )
                    }
                }
            }

        }

      }
    }
  
     

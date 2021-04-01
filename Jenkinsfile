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
                     bat "mvn compile"
                }
            }
    /*stage ('Code Coverage') {
              steps {
                     jacoco changeBuildStatus: true, runAlways: true, skipCopyOfSrcFiles: true
                }
            }*/
      
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
      stage('newman') {
            steps {
                bat 'newman run Restful_Booker.postman_collection1.json --environment Restful_Booker.postman_environment1.json --reporters junit'
            }
            post {
                always {
                        junit '**/*xml'
                    }
                }
        }
     stage('Robot') {
            steps {
                bat 'robot --variable BROWSER:headlesschrome -d Results Tests'
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
  
     

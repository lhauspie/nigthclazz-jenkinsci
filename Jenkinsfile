pipeline {
    agent any

    tools {
        maven 'Maven 3.5.2'
        jdk 'jdk7'
    }

    stages {
        stage ('Initialize') {
            steps {
                sh 'echo "PATH = ${PATH}"'
                sh 'echo "M2_HOME = ${M2_HOME}"'
                sh 'echo "JAVA_HOME = ${JAVA_HOME}"'

                sh 'java -version'
                sh 'mvn -version'
            }
        }

        stage('Build') {
//      agent {
//        dockerfile {
//          filename 'Dockerfile.build'
//          label 'docker'
//        }
//      }
            steps {
                echo 'Building...'
                sh './scripts/build.sh'
            }
            post {
                success {
                    archiveArtifacts 'target/*.jar'
                    stash(name: 'build-result', allowEmpty: true, includes: 'target/**/*')
                }
            }
        }

//    stage('Test') {
//      parallel {
//        stage('Test Java8') {
//          agent {
//            docker {
//              image 'maven:3-jdk-8-alpine'
//              label 'docker'
//            }
//          }
//          steps {
//            unstash 'build-result'
//            echo 'Java8 Testing...'
//            sh './scripts/test.sh'
//          }
//          post {
//            always {
//              junit 'target/surefire-reports/**/*.xml'
//            }
//          }
//        }
//        stage('Test Java7') {
//          agent {
//            node {
//              label 'maven-jdk7'
//            }
//          }
//          steps {
//            unstash 'build-result'
//            echo 'Java7 Testing...'
//            sh './scripts/test.sh'
//          }
//          post {
//            always {
//              junit 'target/surefire-reports/**/*.xml'
//            }
//          }
//        }
//      }
//    }

//    stage('Approval') {
//      agent none
//      when {
//        anyOf {
//          branch 'master'
//          environment name: 'FORCE_DEPLOY', value: 'true'
//        }
//      }
//      steps {
//        input(message: 'Do you approve this release ?', id: 'approve-release', ok: 'Yes !')
//      }
//    }

//    stage('Deploy') {
//      when {
//        anyOf {
//          branch 'master'
//          environment name: 'FORCE_DEPLOY', value: 'true'
//        }
//      }
//      steps {
//        echo 'Deploying...'
//        sh './scripts/deploy.sh'
//      }
//    }
    }
}
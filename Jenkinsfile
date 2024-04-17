pipeline {
  agent any
  stages {
    stage('build') {
      agent {
        docker {
          image 'maven:3.6.3-jdk-11-slim'
        }

      }
      steps {
        echo 'Compiling the code...!!!!'
        sh 'mvn compile'
      }
    }

    stage('test') {
      agent {
        docker {
          image 'maven:3.6.3-jdk-11-slim'
        }

      }
      steps {
        echo 'Running the tests..!!'
        sh 'mvn clean test'
      }
    }

    stage('package') {
      parallel {
        stage('package') {
          agent {
            docker {
              image 'maven:3.6.3-jdk-11-slim'
            }

          }
          when {
            branch 'master'
          }
          steps {
            echo 'Generating artifacts..!!!'
            sh 'mvn package -DskipTests'
            archiveArtifacts 'target/*.war'
            archiveArtifacts 'target/*.war'
          }
        }

        stage('Docker B&P') {
          steps {
            script {
              docker.withRegistry('https://index.docker.io/v1/', 'dockerlogin') {
                def dockerImage = docker.build("shubhamtrainingdevops/sysfoo:v${env.BUILD_ID}", "./")
                dockerImage.push()
                dockerImage.push("latest")
                dockerImage.push("dev")
              }
            }

          }
        }

      }
    }

  }
  tools {
    maven 'Maven 3.6.3'
  }
  post {
    always {
      echo 'This pipeline is completed..'
    }

  }
}
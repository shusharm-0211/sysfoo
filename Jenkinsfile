pipeline {
  agent {
    docker {
      image 'maven:3.6.3-jdk-11-slim'
    }

  }
  stages {
    stage('build') {
      steps {
        echo 'Compiling the code...!!!!'
        sh 'mvn compile'
      }
    }

    stage('test') {
      steps {
        echo 'Running the tests..!!'
        sh 'mvn clean test'
      }
    }

    stage('package') {
      parallel {
        stage('package') {
          
          steps {
            echo 'Generating artifacts..!!!'
            sh 'mvn package -DskipTests'
            archiveArtifacts 'target/*.war'
            archiveArtifacts 'target/*.war'
          }
        }

        stage('error') {
          steps {
            sleep 1
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

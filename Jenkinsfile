pipeline {
  agent any
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

        stage('') {
          steps {
            archiveArtifacts 'target/*.war'
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
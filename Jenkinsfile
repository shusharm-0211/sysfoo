pipeline {
  agent any
  tools{
    maven 'Maven 3.6.3'
  }
  stages{
      stage("build"){
          steps{
              echo 'Compiling the code...!!!!'
              sh 'mvn compile'
          }
      }
      stage("test"){
          steps{
              echo 'Running the tests..!!'
              sh 'mvn clean test'
          }
      }
      stage("package"){
          steps{
              echo 'Generating artifacts..!!!'
              sh 'mvn package -DskipTests'
          }
      }
  }

  post{
    always{
        echo 'This pipeline is completed..'
    }
  }
}

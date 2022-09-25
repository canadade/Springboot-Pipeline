pipeline {
  agent any

  stages {
      stage('Build Artifact') {
            steps {
              bat "mvn clean package -DskipTests=true" //bat has been added in this test
              archive 'target/*.jar' //so that they can be downloaded later
            }
        }   
    }
}

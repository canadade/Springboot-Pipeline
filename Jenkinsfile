pipeline {
  agent any

  stages {
      stage('Build Artifact') {
            steps {
              bat "mvn clean package -DskipTests=true"
              archive 'target/*.jar'
            }
        }
    }
}

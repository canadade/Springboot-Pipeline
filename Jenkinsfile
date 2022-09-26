pipeline {
  agent any

  stages {
      stage('Build Artifact') {
            steps {
              bat "mvn clean package -DskipTests=true" //bat has been added in this test,syst
              archive 'target/*.jar' //so that they can be downloaded later
            }
        }
      stage('Unit Tests') {
            steps {
              bat "mvn test"
            }
            post {
              always {
                junit 'target/surefire-reports/*.xml'
                jacoco execPattern: 'target/jacoco.exec'
              }
            }
        }
      stage('Docker build and push') {
            steps {
              withDockerRegistry([credentialsId: "docker-hub-credentials", url: ""]) {   
                  bat 'docker build -t vignesh0590/numeric-app:latest .'
                  bat 'docker push vignesh0590/numeric-app:latest'
                  }
            }

      }   
      stage('Deploy to Kubernetes'){
            steps{
              script{
                kubeconfig(credentialsId: 'mykubeconfig', serverUrl: 'https://kubernetes.docker.internal:6443') {
                    bat'kubectl apply -f k8s_deployment_service.yaml --insecure-skip-tls-verify'
                }
            }
            
       }
    }
    }
}

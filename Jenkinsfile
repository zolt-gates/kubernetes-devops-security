pipeline {
  agent any

  stages {
      stage('Check maven version') {
            steps {
              sh "mvn --version"
            }
        }  
      stage('Build Artifact') {
            steps {
              sh "mvn clean package -DskipTests=true"
              archive 'target/*.jar'
            }
        } 
      stage('Unit Tests') {
            steps {
              sh "mvn test"
            }
        } 
      stage('Docker Build and Push') {
            steps {
                withDockerRegistry([credentialsId: "docker-hub", url: ""]) {
                    sh "printenv"
                    sh 'docker build -t souljay/numeric-app:""$GIT_COMMIT"" .'
                    sh 'docker push souljay/numeric-app:""$GIT_COMMIT""'
                }
            }
        }   
    }
}

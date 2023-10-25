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
    }
}

pipeline {
  agent any
  #stages are below
  #test one stage
  stages {
      stage('Build Artifact') {
            steps {
              sh "mvn clean package -DskipTests=true"
              archive 'target/*.jar'
            }
        }   
    }
}

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
      stage('SonarQube Analysis') {
              steps {
                sh "mvn sonar:sonar -Dsonar.projectKey=numeric-application -Dsonar.host.url=http://http://devsecops-k8s-2023.eastus.cloudapp.azure.com:9000 -Dsonar.projectName='numeric-application'"
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

      stage('Kubernetes Deployment - DEV') {
            steps {
                withKubeConfig([credentialsId: "kubeconfig"]) {
                    sh "sed -i 's#replace#souljay/numeric-app:${GIT_COMMIT}#g' k8s_deployment_service.yaml"
                    sh "kubectl apply -f k8s_deployment_service.yaml"
                }
            }
        } 
    }
}
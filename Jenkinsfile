pipeline {

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/sd2899/website.git'
      }
    }

    stage('Build image') {
      agent { 
                dockerfile true 
            }
      steps{
        script {
          sudo docker build . -t demoapp
        }
      }
    }

    stage('Kubernetes build') {
      steps {
        script {
          kubernetesDeploy(configs: "kubedeploy.yml", "service.yml")
        }
      }
    }

  }

}

  pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the repository
                checkout scm
            }
        }

        stage('Build') {
            agent { 
                dockerfile true 
            }
            steps { 
            	if (env.BRANCH_NAME == 'master') {
            		sh 'docker build -t my-apache-server .'
                       sh 'docker run -d -p 82:80 my-apache-server'
                } 
                else if (env.BRANCH_NAME == 'develop') {
                	sh 'my-apache-server:develop'
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

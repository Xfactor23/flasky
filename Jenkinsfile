pipeline {
  environment {
    registry = 'xfactor23/flask_app'
    registryCredentails = 'docker'
    cluster_name = 'skillstorm'
  }
  agent {
    node {
      label 'docker'
    }

  }
  stages {
    stage('GIt') {
      steps {
        git(url: 'https://github.com/Xfactor23/flasky.git', branch: 'main')
      }
    }

stage('Build Stage') {
  steps {
    script {
      dockerImage = docker.build(registry)
    }
  }
}
stage('Deploy Stage') {
  steps {
    script {
      docker.withRegistry('', registryCredentails) {
           dockerImage.push()
          }  
          }
        }
stage('kubernetes') {
  steps {
    withCredentials([aws(accessKeyVarible: 'AWS_ACCESS_KEY_ID', credentials:'AWS', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY')]) {
      sh "aws eks update-kubeconfig --region us-east-1 --name ${cluster_name}"
      script{
        try{
          sh "kubectl create namespace ${namespace}"
        }catch (Exception e ) {
          echo "Exception handled"
        }
      }
    }
    sh "kubectl apply -f deployment.yaml -n ${namespace}"
    sh "kubectl -n ${namespace} rollout restart deployment flaskcontainer"
  }
}
}  
}
}  

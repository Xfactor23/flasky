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
}  
}
}  

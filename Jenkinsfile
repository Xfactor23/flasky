pipeline {
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

    stage('Build') {
      steps {
        sh 'docker build -t xfactor23/flask_app .'
      }
    }

    stage('Docker Login') {
      steps {
        sh 'docker login -u xfactor23 -p dckr_pat_Vv4qAiBud5DWEHAlrPs1zJP6rKA'
      }
    }

    stage('Docker Push') {
      steps {
        sh 'docker push xfactor23/flask_app'
      }
    }

  }
}

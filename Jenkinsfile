pipeline {
  agent any
  stages {
    stage ('Supprimer le workspace') {
      steps {
        deleteDir()
      }
    }
    stage ('Checkout SCM') {
      steps {
        git branch: 'main', credentialsId: '9f643542-c4b4-4e98-8868-7fca8e5feae2', url: 'https://github.com/dasilv-h3/projet-dev01.git'
      }
    }
    stage ('Build image docker') {
      steps {
        script {
          sh 'docker build -t myimage_nginx .'
          sh 'docker tag myimage_nginx kevinds:myimage_nginx'
        }
      }
    }
    stage ('Deploiement application') {
      steps {
        script {
          sh 'docker image rm mynginx'
          sh 'docker rm -f $(docker ps -a)'
          sh 'docker run -d --name monapp --hostname monapp -p 8099:80 myimage_nginx'
        }
      }
    }
  }
}

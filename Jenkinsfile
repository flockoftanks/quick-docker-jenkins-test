pipeline {
  agent {
    docker {
      image 'mcr.microsoft.com/dotnet/core/sdk:3.1'
    }

  }
  stages {
    stage('Test') {
      steps {
        sh 'dotnet --version'
      }
    }

  }
}
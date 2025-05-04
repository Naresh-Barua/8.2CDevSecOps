pipeline {
  // Use the official Node image so npm is available
  agent {
    docker {
      image 'node:18-alpine'
      // If your Jenkins user needs extra permissions you can add args,
      // e.g. args '-u root:root', but typically this works out of the box.
    }
  }

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/Naresh-Barua/8.2CDevSecOps.git'
      }
    }

    stage('Install Dependencies') {
      steps {
        sh 'npm install'
      }
    }

    stage('Run Tests') {
      steps {
        sh 'npm test || true'
      }
    }

    stage('Generate Coverage Report') {
      steps {
        sh 'npm run coverage || true'
      }
    }

    stage('NPM Audit (Security Scan)') {
      steps {
        sh 'npm audit || true'
      }
    }
  }
}

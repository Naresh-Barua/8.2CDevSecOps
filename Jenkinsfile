pipeline {
  agent any

  tools {
    // Must match the Name field in your Global Tool Config
    nodejs 'nodejs18'
  }

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main',
            url:   'https://github.com/Naresh-Barua/8.2CDevSecOps.git'
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

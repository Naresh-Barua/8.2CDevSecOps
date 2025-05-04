pipeline {
  agent any

  stages {
    stage('Prepare Environment') {
      steps {
        // Install curl & Node.js 18 on this Debian-based Jenkins container
        sh '''
          apt-get update
          apt-get install -y curl gnupg
          curl -fsSL https://deb.nodesource.com/setup_18.x | bash -
          apt-get install -y nodejs
        '''
      }
    }

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

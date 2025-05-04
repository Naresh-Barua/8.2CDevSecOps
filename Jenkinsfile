pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        // Checkout your GitHub repo
        git branch: 'main', url: 'https://github.com/Naresh-Barua/8.2CDevSecOps.git'
      }
    }

    stage('Install Dependencies') {
      steps {
        // Windows uses bat instead of sh
        bat 'npm install'
      }
    }

    stage('Run Tests') {
      steps {
        // npm test maps to snyk test; exit /b 0 makes the step always succeed
        bat 'npm test || exit /b 0'
      }
    }

    stage('Generate Coverage Report') {
      steps {
        // no coverage script defined upstream, so ignore errors
        bat 'npm run coverage || exit /b 0'
      }
    }

    stage('NPM Audit (Security Scan)') {
      steps {
        // show vulnerabilities, but don’t fail the build
        bat 'npm audit || exit /b 0'
      }
    }
  }
}

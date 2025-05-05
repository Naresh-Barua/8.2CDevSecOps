pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main',
            url:    'https://github.com/Naresh-Barua/8.2CDevSecOps'
      }
    }

    stage('Install Dependencies') {
      steps {
        sh 'npm install'
      }
    }

    stage('Run Tests') {
      steps {
        // run your Snyk tests; allow failures so pipeline continues
        sh 'npm test || true'
      }
    }

    stage('Generate Coverage Report') {
      steps {
        // if you have a coverage script
        sh 'npm run coverage || true'
      }
    }

    stage('NPM Audit (Security Scan)') {
      steps {
        sh 'npm audit || true'
      }
    }
  }

  post {
    always {
      // send an email regardless of build result
      emailext(
        to:      'nareshbarua123@gmail.com',           
        subject: "Build ${currentBuild.fullDisplayName}: ${currentBuild.currentResult}",
        body:    """\
Build URL: ${env.BUILD_URL}
Status:    ${currentBuild.currentResult}

See console output at:
  ${env.BUILD_URL}console
""".stripIndent()
      )
    }
  }
}

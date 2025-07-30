pipeline {
  agent {
    docker {
      image 'node:20'
    }
   }

  environment {
    FIREBASE_TOKEN = credentials('firebase-token')
  }

  stages {
    stage('Build') {
      steps {
        echo 'Install Firebase CLI'
        sh 'npm install -g firebase-tools'
      }
    }
    stage('Deploy to Testing') {
      steps {
        echo 'Deploying to TESTING...'
        sh 'firebase deploy --only hosting --project testing --token=$FIREBASE_TOKEN'
      }
    }
    stage('Deploy to Staging') {
      steps {
        echo 'Deploying to STAGING...'
        sh 'firebase deploy --only hosting --project staging --token=$FIREBASE_TOKEN'
      }
    }
    stage('Deploy to Production') {
      steps {
        input message: 'Deploy to PRODUCTION?', ok: 'Yes, deploy'
        echo 'Deploying to PRODUCTION...'
        sh 'firebase deploy --only hosting --project prod --token=$FIREBASE_TOKEN'
      }
    }
  }
}


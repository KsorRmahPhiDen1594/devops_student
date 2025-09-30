pipeline {
  agent any

  environment {
    NODE_ENV = 'production'
  }

  stages {
    stage('📥 Clone Repo') {
      steps {
        git 'https://github.com/KsorRmahPhiDen1594/devops_student.git'
      }
    }

    stage('📦 Install Dependencies') {
      steps {
        sh 'npm install'
      }
    }

    stage('🏗️ Build App') {
      steps {
        sh 'npm run build'
      }
    }

    stage('🧪 Run Tests') {
      when {
        expression { fileExists('jest.config.js') || fileExists('test') }
      }
      steps {
        sh 'npm test'
      }
    }

    stage('🚀 Deploy App') {
      steps {
        sh '''
          if ! command -v pm2 &> /dev/null; then
            npm install -g pm2
          fi
          
          pm2 delete nextjs-app || true
          pm2 start npm --name "nextjs-app" -- start
        '''
      }
    }

    stage('✅ Done') {
      steps {
        echo '🎉 Next.js build & deploy completed!'
      }
    }
  }
}

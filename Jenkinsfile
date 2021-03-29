pipeline {
  agent any
  stages {
    stage('Build') {
      post {
        failure {
          script {
            message="failure"
          }

        }

        success {
          script {
            message="Success"
          }

        }

      }
      steps {
        bat 'C:\\\\Users\\\\sony\\\\Desktop\\\\gradle-5.6-bin\\\\gradle-5.6\\\\bin\\\\gradle build'
        bat 'C:\\\\Users\\\\sony\\\\Desktop\\\\gradle-5.6-bin\\\\gradle-5.6\\\\bin\\\\gradle javadoc'
        archiveArtifacts 'build/libs/*.jar'
        archiveArtifacts 'build/docs/javadoc/*'
        junit 'build/test-results/test/*.xml'
      }
    }

    stage('Mail Notification') {
      steps {
        mail(subject: 'Build Notification', body: "${message}", from: 'ga_bendjeddou@esi.dz', to: 'hl_medjahed@esi.dz')
      }
    }

    stage('Code Analysis') {
      parallel {
        stage('Code Analysis') {
          steps {
            withSonarQubeEnv('sonar') {
              bat 'C:\\\\Users\\\\sony\\\\Desktop\\\\gradle-5.6-bin\\\\gradle-5.6\\\\bin\\\\gradle sonarqube'
            }

            waitForQualityGate true
          }
        }

        stage('Test Reporting') {
          steps {
            cucumber '**/*.json'
          }
        }

      }
    }

    stage('Deployment') {
      when {
        branch 'master'
      }
      steps {
        bat 'C:\\\\Users\\\\sony\\\\Desktop\\\\gradle-5.6-bin\\\\gradle-5.6\\\\bin\\\\gradle publish'
      }
    }

    stage('slack ') {
      when {
        branch 'master'
      }
      steps {
        slackSend(baseUrl: 'https://hooks.slack.com/services', teamDomain: 'aya', token: 'TFL2J22BW/B01SM0XKHMY/HHlpYefl0q0z1i4XD4lTNp4h', message: 'deployer', channel: 'aya')
      }
    }

  }
}
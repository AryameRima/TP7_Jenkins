pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        powershell 'C:\\\\Users\\\\sony\\\\Desktop\\\\gradle-5.6-bin build'
        powershell 'C:\\\\Users\\\\sony\\\\Desktop\\\\gradle-5.6-bin javadoc'
        archiveArtifacts 'build/libs/*.jar'
        archiveArtifacts 'build/docs/javadoc/*'
      }
    }

    stage('Mail Notification') {
      steps {
        mail(subject: 'Test', body: 'Test', to: 'hl_medjahed@esi.dz', from: 'ga_bendjeddou@esi.dz')
      }
    }

  }
}
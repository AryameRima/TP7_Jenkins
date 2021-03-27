pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        powershell 'gradle build'
        powershell 'gradle javadoc'
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
pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        archiveArtifacts 'build/libs/*.jar'
        archiveArtifacts 'build/docs/javadoc/*'
        pwsh 'gradle build'
        pwsh 'gradle javadoc'
      }
    }

    stage('Mail Notification') {
      steps {
        mail(subject: 'Test', body: 'Test', to: 'hl_medjahed@esi.dz', from: 'ga_bendjeddou@esi.dz')
      }
    }

  }
}
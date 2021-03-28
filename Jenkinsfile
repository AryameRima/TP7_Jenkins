pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        bat 'C:\\\\Users\\\\sony\\\\Desktop\\\\gradle-5.6-bin\\\\gradle-5.6\\\\bin\\\\gradle build'
        bat 'C:\\\\Users\\\\sony\\\\Desktop\\\\gradle-5.6-bin\\\\gradle-5.6\\\\bin\\\\gradle javadoc'
        archiveArtifacts 'build/libs/*.jar'
        archiveArtifacts 'build/docs/javadoc/*'
      }
    }

    stage('Mail Notification') {
      steps {
        mail(subject: 'Test', body: 'Test', to: 'hl_medjahed@esi.dz', from: 'ga_bendjeddou@esi.dz')
      }
    }

    stage('Code Analysis') {
      parallel {
stage('Code Analysis'){
steps{
withSonarQubeEnv('SonarQube'){
bat 'C:\\\\Users\\\\sony\\\\Desktop\\\\gradle-5.6-bin\\\\gradle-5.6\\\\bin\\\\gradle sonarqube'
}
script {
echo "test2"
def qg= waitForQualityGate()
if(qg.status !='ok')
{
error "Pipeline aborted due to quality gate failure:${qg.status}"
echo "test3"}
    }
}
}
  }
}

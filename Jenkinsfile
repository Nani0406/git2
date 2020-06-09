pipeline {
   agent any

   stages {
      stage('Git Checkout') {
         steps {
            git 'https://github.com/Nani0406/mvn_sonar.git'
         }
      }
      stage('Build') {
        steps {
            withSonarQubeEnv('sonar') {
                sh '/opt/maven/bin/mvn clean verify sonar:sonar'
            }
        }
      }
      stage('Quality Gate') {
          steps {
              timeout(time: 1, unit: 'MINUTES') {
                      waitForQualityGate abortPipeline: true
              }
          }
      }
      stage('Deploy') {
         steps {
            sh '/opt/maven/lib/mvn clean deploy'
         }
      }
      stage('Release') {
         steps {
            sh 'export JENKINS_NODE_COOKIE=dontKillMe'
         }
      }
  }
}

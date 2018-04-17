pipeline {
  agent any
  stages {
    stage('Initialize') {
      steps {
        sh 'mvn clean'
      }
    }
    stage('Test') {
      parallel {
        stage('Test') {
          steps {
            sh 'mvn test'
          }
        }
        stage('sonar') {
          steps {
            withSonarQubeEnv('sonar-local'){
               sh 'mvn clean package sonar:sonar'
            }
          }
        }
      }
    }
    stage('validate') {
      steps {
        waitForQualityGate true
      }
    }
    stage('install') {
      steps {
        sh 'mvn install'
      }
    }
    stage('Clean') {
      steps {
        sh 'mvn clean'
      }
    }
    stage('end') {
      steps {
        cleanWs(cleanWhenSuccess: true)
      }
    }
  }
}

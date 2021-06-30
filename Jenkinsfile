pipeline {
  agent any
  stages {
    stage('Unit Test') {
      steps {
        sh 'mvn clean test'
      }
    }
    stage('Deploy Standalone') {
      steps {
        sh 'mvn deploy -P standalone'
      }
    }
    stage('Deploy ARM') {
      environment {
        ANYPOINT_CREDENTIALS = credentials('anypoint.credentials')
      }
      steps {
        sh 'mvn deploy -P arm -Darm.target.name=local-3.9.0-ee -Danypoint.username=${ANYPOINT_CREDENTIALS_USR} -Danypoint.password=${ANYPOINT_CREDENTIALS_PSW}'
      }
    }
    stage('Deploy CloudHub') {      steps {
        sh 'mvn clean package deploy -P cloudhub -DmuleDeploy -DskipTests -Dmule.version=4.3.0-20210119 -Danypoint.username=Rajee8952 -Danypoint.password=Rakhi@8466 -Dappname=CICDDemo29June2021 -Denv=Sandbox -Dbusiness=xyz -DvCore=Micro -Dworkers=1'
      }
    }
  }
}
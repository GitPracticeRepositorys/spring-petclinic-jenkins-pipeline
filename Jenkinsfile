pipeline {
  agent any
  tools {
    maven 'MAVEN_3.6.3'
    jdk 'jdk8'
  } 
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/GitPracticeRepositorys/spring-petclinic-jenkins-pipeline.git'
      }
    }
    stage('Compile') {
       steps {
         sh 'mvn compile' //only compilation of the code
       }
    }
    stage('Test') {
      steps {
        sh '''
        mvn clean install
        ls
        pwd
        ''' 
        //if the code is compiled, we test and package it in its distributable format; run IT and store in local repository
      }
    }
    stage('docker image build') {
            steps {
                sh 'docker image build -t shivakrishna99/spring-pet-clinic .'
            }
        }
        stage('push image to registry') {
            steps {
                sh 'docker image push shivakrishna99/spring-pet-clinic'
            }
        }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $registry:latest"
      }
    }
  }
}

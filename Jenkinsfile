pipeline {
  environment {
    registry = "oussama24/docker_from_pipeline"
    registryCredential = 'dockerfrompipeline'
    dockerImage = 'pipeline_cicd:1.0'
  }
  agent any
  
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/oussama24bessaad/-docker_from_pipeline.git'
      }
    }
    stage('Build (npm)') {
       steps {
         sh 'npm cache clean --force'
         sh 'npm install -g @angular/cli@latest'
       }
    }
    
    stage('Images List') {
      steps {
        sh 'docker images oussama24/docker_from_pipeline'
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Pushing Image') {
      steps{
         script {
            docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
  
}
}

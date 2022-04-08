pipeline{
  environment{
     imageName = "28071989/docker-jenkins-project"
     registryCredential = 'dockerhub'
     dockerImage =''
  }
  agent any
   stages {
    stage('Cloning Git') {
      steps {
        git([url: 'https://github.com/HimanshuSharma1681//docker-demo.git', branch: 'master'])
      }
    }
     
     stage('Building image') {
      steps{
        script {
          dockerImage = docker.build imageName
        }
      }
    }
   stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push("$BUILD_NUMBER")
             dockerImage.push('latest')
 
          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $imageName:$BUILD_NUMBER"
         sh "docker rmi $imageName:latest"
 
      }
    }
  }
}

pipeline{
  agent{
    node{
      label '410977010'
    }
  }
  environment{
    DOCKERHUB_CREDENTIALS = credentials('410977010-dockerhub')
  }
  options {
      skipDefaultCheckout(true)
  }
  stages{
    stage('Clean old DOCs & chekcout SCM'){
      steps{
        // two critical functions
      }
    }
    stage('verify tools'){
     steps{
       sh '''
       docker info
       docker version
       docker-compose version
       '''
     }  
    }
    stage('Login Dockerhub'){
      steps{
        sh '''
          echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin
        '''
      }
    }
    stage('Build image for application'){
      steps{
        sh '''
          // your command
        '''
      }
    }
    stage('Rename && Push image to Dockerhub'){
      steps{
        sh '''
          docker tag  <your_job_name>_ci4_service:<your_tag> <your_DockerHUBID>/<your_job_name>_ci4_service:<your_tag>
          docker push <your_DockerHUBID>/<your_job_name>_ci4_service:<your_tag>
        '''
      }
    }
    stage('Start Container'){
      steps{
        sh '''
        docker-compose up -d
        '''
      }
    }
    stage('Check Container'){
      steps{
        sh '''
           // your command
        '''
      }
    }
   }
   post {
        always {
          sh '''
          docker-compose down
          docker system prune -a -f
          docker logout
          '''
        }
      }
}
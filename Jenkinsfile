node{
  def Namespace = "docker-test"
  def ImageName = "amit3189/k8_docker_image"
  def Creds	= "dockerhub_creds"
  def imageTag = "1.0"
  
 try{
  stage('Checkout'){
      git 'https://github.com/amit3189/mk-k8-ci-cd.git'
      //sh "git rev-parse --short HEAD > .git/commit-id"
      //imageTag= readFile('.git/commit-id').trim()



  }


  stage('RUN Unit Tests'){
      sh "npm install"
      sh "npm test"
  }
  stage('Docker Build, Push'){
    withDockerRegistry([credentialsId: "${Creds}", url: 'https://index.docker.io/v1/']) {
      sh "docker build -t ${ImageName}:${imageTag} ."
      sh "docker push ${ImageName}"
        }

    }
     } catch (err) {
      currentBuild.result = 'FAILURE'
    }
}

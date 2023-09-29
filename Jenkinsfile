node {
  def app

  stage('Clone repository'){


    checkout scm
  }
  
  stage('Build Image'){

    app = docker.build("dhysenaj/test")
  }
  
  stage('Test Image'){

    app.inside{
      sh 'echo "Test successfull"'
    }
  }
  
  stage('Push Image'){

    docker.withRegistry('https://registry.hub.docker.com','dockerhub'){
      app.push("${env.BUILD_NUMBER}")
    }
  }
  
  stage('Trigger ManifestsUpdate'){
      echo "triggering updatemanifestjob"
      build job: 'updatemanifest', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
  }
}

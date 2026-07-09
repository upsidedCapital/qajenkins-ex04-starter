pipeline {
  agent any
  environment {
    registry = "ex04"
    dockerImage = ""
  }
  stage ('Docker Build'){
    steps{
        script {
            dockerImage = docker.build(registry)
            dockerImage.tag("${env.BUILD_NUMBER}")
        }
    }
}
      }
    }
    stage("Scan Image") {
      steps {
        sh "echo 'Scan Image...'"
      }
    }
  }
}

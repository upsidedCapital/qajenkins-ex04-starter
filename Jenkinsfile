pipeline {
    agent any

    environment {
        registry = "ex04"
        dockerImage = ""
    }

    stages {

        stage('Docker Build') {
            steps {
                script {
                    dockerImage = docker.build(registry)
                    dockerImage.tag("${env.BUILD_NUMBER}")
                }
            }
        }

       stage('Scan Image') {
    steps {
      grypeScan scanDest: "docker:${registry}:${BUILD_NUMBER}", repName: 'scanResult.txt', autoInstall:true
    }
}

    }
}

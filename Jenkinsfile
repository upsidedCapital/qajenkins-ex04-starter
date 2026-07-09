pipeline {
    agent any

    environment {
        registry = "ex04"
        dockerImage = ""
    }

    stages {
        stage("Validate With Terrascan") {
            steps {
                sh 'terrascan scan -i docker'
            }
        }

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
                grypeScan(
                    scanDest: "docker:${registry}:${env.BUILD_NUMBER}",
                    repName: 'scanResult.txt',
                    autoInstall: true
                )
            }
        }
    }

    post {
        always {
            recordIssues(
                qualityGates: [
                    [
                        criticality: 'FAILURE',
                        integerThreshold: 100,
                        threshold: 100.0,
                        type: 'TOTAL_HIGH'
                    ],
                    [
                        criticality: 'FAILURE',
                        integerThreshold: 5,
                        threshold: 5.0,
                        type: 'NEW'
                    ]
                ],
                sourceCodeRetention: 'LAST_BUILD',
                tools: [grype()]
            )
        }
    }
}

pipeline {
    agent none
    stages {
        stage('Build') {
            agent {
              label "build"
            }
            steps {
                cmakeBuild(
                  installation: 'InSearchPath'
                  )
            }
        }
        stage('Upload') {
            agent {
              label "test"
            }
            steps {
                sh 'echo Deploying'
            }
        }
    }
}

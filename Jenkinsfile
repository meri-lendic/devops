pipeline {
    agent none
    stages {
        stage('Build') {
            agent {
              label "build"
            }
            steps {
                echo "buid"
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

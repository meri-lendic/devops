pipeline {
    agent none
    stages {
        stage('Build') {
            agent {
              label "build"
            }
            steps {sh 'gcc --version'}
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

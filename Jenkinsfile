pipeline {
    agent none
    stages {
        'Build' {
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

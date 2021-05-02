pipeline {
    agent none
    stages {
        stage('Build') {
            agent {
              label "build"
            }
            
            steps {
                sh 'gcc "main.c" -o "main.exe"'
                cmakeBuild(
            installation: 'CMakeLists.txt'
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

pipeline {
    agent none
    stages {
        stage('Build') {
            agent {
              label "build"
            }
            
            steps {
                sh 'gcc "main.c" -o "main.exe"'
                sh 'make "main.exe"'
                sh './main.exe'

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

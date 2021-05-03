pipeline {
    agent none
    stages {
        stage('Buuuuild') {
            agent {
              label "build"
            }
            
            steps {
                sh 'gcc main.c -o main.exe'
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

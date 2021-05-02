pipeline {
    agent none
    stages {
        stage('Build') {
            agent {
              label "build"
            }
            
            steps {
                sh 'gcc "main.c" -o main'
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

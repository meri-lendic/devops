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
                echo 'Pulling...' + env.BRANCH_NAME

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

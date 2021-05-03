def getGitBranchName() {
    return scm.branches[0].name
}
pipeline {
    agent any
    stages {
        stage('Build') {
            agent {
              label "build"
            }
            steps {
                sh 'gcc main.c -o main.exe'
                sh './main.exe'
                sh 'pwd'
                echo "Pulling... " + env.GIT_BRANCH
                  }
        }
        stage('Upload') {
            steps {
                sh 'echo Deploying'
                }
        }
    }
}

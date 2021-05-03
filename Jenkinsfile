def getGitBranchName() {
    return scm.branches[0].name
}
pipeline {
    agent none
    stages {
        agent {
              label "build"
            }
        stage('Build') {
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

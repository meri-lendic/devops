def getGitBranchName() {
    return scm.branches[0].name
}
pipeline {
    agent none
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
            agent {
              label "build"
            }
            steps {
                sh 'echo Deploying' getGitBranchName()
                }
        }
    }
}

def getGitBranchName() {
    return scm.branches[0].name
}
pipeline {
    agent none
    environment {
    FULL_PATH_BRANCH = "${sh(script:'git name-rev --name-only HEAD', returnStdout: true)}"
    GIT_BRANCH = FULL_PATH_BRANCH.substring(FULL_PATH_BRANCH.lastIndexOf('/') + 1, FULL_PATH_BRANCH.length())
  }
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
                sh 'echo Deploying' + getGitBranchName()
                }
        }
    }
}

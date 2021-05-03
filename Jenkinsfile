def getGitBranchName() {
    return scm.branches[0].name
}
pipeline {
    agent none
    stages {
        stage('Build') {
            //define an agent to run this stage
            agent {
              label "build"
            }
            steps {
                //compile main.c and execute it
                sh '''
                    gcc main.c -o main.exe
                    ./main.exe
                    '''
                echo "Build stage finished! " + env.GIT_BRANCH
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

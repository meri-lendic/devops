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
                echo "Pulling... " + env.GIT_BRANCH 
        }
        stage('Upload') {
            agent {
              label "test"
            }
            script{
            def getGitBranchName() {
    return scm.branches[0].name
            }}
            steps {
                sh 'echo Deploying' + getGitBranchName
            }
            
        }
    }
}
    

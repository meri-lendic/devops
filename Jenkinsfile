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
                        
            withCredentials([string(credentialsId: 'bf3b667a-5110-4b7f-afe7-357e8d5ef351', variable: 'TokenForGitHub')]) {
              sh '''
                curl -XPOST -H "Authorization: token "$TokenForGitHub" https://github.com/meri-lendic/devops/statuses/$(git rev-parse HEAD) -d "{
                    \"state\": \"failure\",
                    \"target_url\": \"${BUILD_URL}\",
                        \"description\": \"The build has failed!\"
                    }"
                '''
                    }
        }
    }
    }
}

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
                def branch_nem = scm.branches[0].name
                if (branch_nem.contains("*/")) {
                        branch_nem = branch_nem.split("\\*/")[1]
                        }
                        echo branch_nem

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

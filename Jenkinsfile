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
		   post {
    				failure {
                  withCredentials([string(credentialsId: 'bf3b667a-5110-4b7f-afe7-357e8d5ef351', variable: 'TokenForGitHub')]) {
              sh '''
                curl -XPOST -H "Authorization: token "$TokenForGitHub" https://api.github.com/meri-lendic/devops/$(git rev-parse HEAD) -d "{
                    \"state\": \"failure\",
                    \"target_url\": \"${BUILD_URL}\",
                        \"description\": \"The build has failed!\"
                    }"
                '''
                    }
    }
			   success {
                  withCredentials([string(credentialsId: 'bf3b667a-5110-4b7f-afe7-357e8d5ef351', variable: 'TokenForGitHub')]) {
              sh '''
                curl -XPOST -H "Authorization: token "$TokenForGitHub" https://api.github.com/repos/meri-lendic/devops/$(git rev-parse HEAD) -d "{
                    \"state\": \"success\",
                    \"target_url\": \"${BUILD_URL}\",
                        \"description\": \"The build has succeeded!\"
                    }"
                '''
                    }
    }
  }
        }
        stage('Upload') {
            agent {
              label "build"
            }
            steps {
                s3Upload consoleLogLevel: 'INFO', 
	            dontSetBuildResultOnFailure: false, 
	            dontWaitForConcurrentBuildCompletion: false, 
	            entries: [[bucket: getGitBranchName(), 
	            excludedFile: '', flatten: false, gzipFiles: false, 
	            keepForever: false, managedArtifacts: false, noUploadOnFailure: true, 
	            selectedRegion: 'eu-central-1', showDirectlyInBrowser: false, sourceFile: '**/*.exe', 
                storageClass: 'STANDARD', uploadFromSlave: true, useServerSideEncryption: true]], 
	            pluginFailureResultConstraint: 'FAILURE', profileName: 'S3-Deployment', userMetadata: []
                     
        }
    }
    }
 
}

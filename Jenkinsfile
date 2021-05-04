def getGitBranchName() {
    return scm.branches[0].name
}
pipeline {
    agent none
    stages {
        stage('Build') {
		environment {
			GIT_HUB_API= "https://api.github.com/repos/meri-lendic/devops/statuses/$GIT_COMMIT"
		}
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
                echo "Build stage finished!"
                  }
		   post {
			   //notifying GitHub in case of the failure
			   failure {
                  withCredentials([string(credentialsId: 'bf3b667a-5110-4b7f-afe7-357e8d5ef351', variable: 'TokenForGitHub')]) {
              sh '''
	      	      curl -X POST -H "Authorization: Token "$TokenForGitHub"" --data "{\\"state\\": \\"failure\\", \\"target_url\\": \\"${BUILD_URL}\\",
		    \\"description\\": \\"The build has failed!\\, \\"context\\": \\"jenkins build status\\"}" --url $GIT_HUB_API
	         '''
                    }
			   }
			   //notifying GitHub in case of the success
			   success {
                  withCredentials([string(credentialsId: 'bf3b667a-5110-4b7f-afe7-357e8d5ef351', variable: 'TokenForGitHub')]) {
              sh '''
	      curl -X POST -H "Authorization: Token "$TokenForGitHub"" --data "{\\"state\\": \\"success\\", \\"target_url\\": \\"${BUILD_URL}\\",
		    \\"description\\": \\"The build was successful!\\", \\"context\\": \\"jenkins build status\\"}" --url $GIT_HUB_API
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
		    //upload into s3
                s3Upload consoleLogLevel: 'INFO', 
	            dontSetBuildResultOnFailure: false, 
	            dontWaitForConcurrentBuildCompletion: false, 
	            entries: [[bucket: deployment-main.exe, 
	            excludedFile: '', flatten: false, gzipFiles: false, 
	            keepForever: false, managedArtifacts: false, noUploadOnFailure: true, 
	            selectedRegion: 'eu-central-1', showDirectlyInBrowser: false, sourceFile: '**/*.exe', 
                storageClass: 'STANDARD', uploadFromSlave: true, useServerSideEncryption: true]], 
	            pluginFailureResultConstraint: 'FAILURE', profileName: 'S3-full-access', userMetadata: []
                     
        }
    }
    }
 
}

pipeline {
    agent none
    stages {
        stage('Build') {
            agent {
              label "build"
            }
            
            steps {
                sh 'gcc --version'
                 cmakeBuild
                    generator: 'Ninja',
                    buildDir: 'build',
                    sourceDir: 'source',
                    installation: 'InSearchPath',
                        steps: [
                                [args: 'all install', envVars: 'DESTDIR=${WORKSPACE}/artifacts']
                                ]
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

pipeline {
    agent {
        docker { 
            image 'docksal/ci-agent:edge-base'
            alwaysPull true
        }
    }

    environment { 
        DEBUG = 1
    }
    
    stages {
        stage('Test') {
            steps {
                sh 'whoami'
                sh 'pwd'
                sh 'ls -la'
                sh 'env'
                sh "echo ${BRANCH_NAME}"
                sh "echo ${env.BRANCH_NAME}"
            }
        }

        stage('Sandbox build') {
            steps {
                withCredentials([string(credentialsId: 'DOCKSAL_HOST_SSH_KEY', variable: 'DOCKSAL_HOST_SSH_KEY')]) {
                    sh '''#!/bin/bash
                        source build-env
                        env
                        sandbox-init
                    '''
                }
            }
        }
    }
}

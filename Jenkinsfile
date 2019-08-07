pipeline {
    agent {
        docker { image 'docksal/ci-agent:edge-base' }
    }

    //parameters {
    //    text(name: 'SSH_KEY', defaultValue: '', description: 'Sandbox server SSH private key (base64 encoded)')
    //}    
    
    environment { 
        DEBUG = 1
    }
    
    stages {
        stage('Checkout code') {
            steps {
                checkout scm
            }
        }

        stage('Test') {
            steps {
                sh 'whoami'
                sh 'pwd'
                sh 'ls -la'
                sh 'env'
                sh "echo ${env.BRANCH_NAME}"
            }
        }

        stage('Sandbox build') {
            steps {
                //withCredentials([string(credentialsId: 'DOCKSAL_HOST', variable: 'DOCKSAL_HOST'), string(credentialsId: 'DOCKSAL_HOST', variable: 'DOCKSAL_HOST_SSH_KEY')]) {
                    sh '''#!/bin/bash
                        #export DOCKSAL_HOST_SSH_KEY=${SSH_KEY}
                        source build-env
                        env
                        sandbox-init
                    '''
                //}
            }
        }
    }
}

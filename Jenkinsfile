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
        //stage('Checkout code') {
        //    steps {
        //        checkout scm
        //    }
        //}

        stage('Test') {
            steps {
                sh '''#!/bin/bash
                    whoami
                    pwd
                    ls -la
                    env
                    echo ${BRANCH_NAME}
                '''
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

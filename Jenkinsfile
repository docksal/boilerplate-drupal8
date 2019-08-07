pipeline {
    agent {
        docker { image 'docksal/ci-agent:edge-base' }
    }

    parameters {
        text(name: 'SSH_KEY', defaultValue: '', description: 'Sandbox server SSH private key (base64 encoded)')
    }    
    
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

        stage('Secrets') {
            steps {
                withCredentials([string(credentialsId: 'DOCKSAL_HOST', variable: 'DOCKSAL_HOST'), string(credentialsId: 'DOCKSAL_HOST', variable: 'DOCKSAL_HOST_SSH_KEY')]) {
                    sh '''#!/bin/bash
                        export DOCKSAL_HOST_SSH_KEY=${params.SSH_KEY}
                        env
                        source build-env
                        env
                        build-exec 'hostname'
                    '''
                }
            }
        }

        stage('Build sandbox') {
            steps {
                sh '''#!/bin/bash
                    env
                '''
            }
        }
    }
}

pipeline {
    agent {
        docker { image 'docksal/ci-agent:edge-base' }
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

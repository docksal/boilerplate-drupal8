pipeline {
    agent {
        docker { image 'docksal/ci-agent:1.7-base' }
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
                    '''
                }
            }
        }

        stage('Build sandbox') {
            steps {
                sh '''#!/bin/bash
                    source build-env
                    env
                '''
            }
        }
    }
}

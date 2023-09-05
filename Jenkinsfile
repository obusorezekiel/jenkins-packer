pipeline {
    agent any

    stages {
        stage("Git Clone") {
            steps {
                git branch: "main", url: 'https://github.com/obusorezekiel/jenkins-packer.git'
            }
        }

        stage('Install Packer'){
            steps {
                script {
                    sh'''#!/bin/bash 
                        sudo curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
                        sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
                        sudo apt-get update && sudo apt-get install packer
                    '''
                }
            }
        }

        stage('Packer validate') {
            steps {
                script {
                sh'''#!/bin/bash 
                        packer validate packer.json
                    '''
                }
            }
        }

        stage('packer build') {
            steps {
                script {
                    sh'''#!/bin/bash 
                        packer build packer.json
                    '''
                }
            }
        }
    }
}
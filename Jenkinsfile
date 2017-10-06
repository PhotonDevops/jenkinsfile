#!/usr/bin/env groovy

pipeline {
    agent any
    
    stages {
        stage('Unitest-Manulife') {
            steps {
                echo 'get the code from github repository..'
                git branch: 'dev', credentialsId: 'Github', url: 'https://github.com/RatihNurmalasari/m-insurance-service.git'
            }
        }
        stage('Build') {
            step {
                echo 'Building..'
            }
        }
    }
}

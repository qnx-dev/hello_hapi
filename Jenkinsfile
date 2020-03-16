#!/usr/bin/env groovy

pipeline {

    agent any
    
    stages {
        stage('Build') {
            steps {
                nodejs('nodejs-default') {
                    echo 'Building...'
                    sh 'npm install'
                }
            }
        }
        stage('Test') {
            steps {
                nodejs('nodejs-default') {
                    echo 'Testing...'
                    sh 'npm test'
                }
            }
        }
    }
    
    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            mail to: "mark_paderes@questronix.com.ph", 
                from: 'developer@questronix.com.ph',
                subject: "ERROR CI: Project name -> ${env.JOB_NAME}",
                body: "<b>Example</b><br>\n\n<br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL de build: ${env.BUILD_URL}", 
                cc: '', charset: 'UTF-8',  mimeType: 'text/html', replyTo: ''
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}

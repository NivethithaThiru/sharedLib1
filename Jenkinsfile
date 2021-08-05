@Library('jenkins-groovy-sharedLibrary')_

pipeline {
    agent any
    stages {
        stage('Demo') {
            steps {
                echo 'Hello World'
                hello 'Nivethitha Thirumurugan'
            }
        }
        stage('Build') {
            steps {
                script{
                    def filePath = readFile "AppReleases.csv" 
                    def lines = filePath.readLines() 
                    for (line in lines) { 
                        println "$line"
                    } 
                }
            }
        }
        stage('Email Notification') {
            steps {
                echo 'Sending Email !!'
                emailext ( attachLog: true, 
                body: """<p>EXECUTED: Job <b>\'${env.JOB_NAME} : ${env.BUILD_NUMBER}\'</b></p>
                <p>View console output at <a href="${env.BUILD_URL}">Jenkins ${env.JOB_NAME}:${env.BUILD_NUMBER}</a></p>""",
                recipientProviders: [requestor(), buildUser()],
                replyTo: 'do-not-reply@company.com', 
                subject: """Status: ${currentBuild.result?:'SUCCESS'} - Job \'${env.JOB_NAME}:${env.BUILD_NUMBER}\'""",
                to: 'nivethithathiru1@gmail.com' )
            }
        }
    }
}

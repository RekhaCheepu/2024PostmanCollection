pipeline {
    agent any
    stages {

        stage('Build') {
            steps {
                echo("build the war")
            }
        }

        stage("Deploy to QA"){
            steps{
                echo("deploy to qa")
            }
        }

        stage('Checkout') {
            steps {
                git url: 'https://github.com/RekhaCheepu/2024PostmanCollection'
            }
        }
        stage('Run api test cases') {
            steps {
                bat 'newman run ./GoRestAPIs_workflow.postman_collection.json  -e ./GORestWorkflow.postman_environment.json -n 1 -r htmlextra,cli --reporter-htmlextra-export ./results/booking_report.html'
            }
        }
        stage('Publish HTML Extra Report'){
            steps{
                     publishHTML([allowMissing: false,
                                  alwaysLinkToLastBuild: false, 
                                  keepAll: true, 
                                  reportDir: 'results', 
                                  reportFiles: 'booking_report.html', 
                                  reportName: 'HTML Extra API Report', 
                                  reportTitles: ''])
            }
        }

        stage("Deploy to PROD"){
            steps{
                echo("deploy to PROD")
            }
        }
    }
}
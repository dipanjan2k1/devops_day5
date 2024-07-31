pipeline {
    agent any
    stages {
        stage('Unit Test') {
            steps {
                build job: 'QA_UNIT_TEST'
            }
        }
        stage('Metrics Check') {
            steps {
                build job: 'QA_METRICS_CHECK'
            }
        }
        stage('Package') {
            steps {
                build job: 'QA_PACKAGE'
            }
        }
    }
    post {
        always {
            script {
                // Archive the reports
                archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
                cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: '**/target/site/cobertura/coverage.xml'
            }
        }
    }
}

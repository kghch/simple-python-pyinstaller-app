pipeline {
    agent any
    
    stages {
        stage('A') {
            stages {
                stage('A1') {
                    steps {
                        sleep 1
                    }
                }
                stage('A2') {
                    steps {
                        sleep 1
                    }
                }
            }
        }
    }
    post {
        always {
            influxDbPublisher(selectedTarget: 'jenkins', measurementName: 'total_table', customData: myFields) null
        }
    }
}
 

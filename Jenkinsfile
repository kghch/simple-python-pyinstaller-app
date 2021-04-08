pipeline {
    agent any
    
    stages {
        stage('A') {
            stages {
                stage('A1') {
                    steps {
                        sleep 1
                    }
                    post {
                      always {
                        influxDbPublisher(selectedTarget: 'jenkins', measurementName: 'a1_table')
                      }
                    }
                }
                stage('A2') {
                    steps {
                        sleep 1
                    }
                    post {
                      always {
                        influxDbPublisher(selectedTarget: 'jenkins', measurementName: 'a2_table')
                      }
                    }
                }
            }
        }
    }
    post {
        always {
            influxDbPublisher(selectedTarget: 'jenkins', measurementName: 'total_table')
        }
    }
}


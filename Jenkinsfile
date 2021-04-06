pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                sh 'echo Running build.'
            }
        }
        post {
          always {
            influxDbPublisher(selectedTarget: 'jenkins', measurementName: 'build_table')
          }
        }
        stage('test') {
            steps {
                sh 'echo Running test.'
            }
        }
        post {
          always {
            influxDbPublisher(selectedTarget: 'jenkins', measurementName: 'test_table')
          }
        }        
    }
    post {
      always {
        influxDbPublisher(selectedTarget: 'jenkins')
      }
    }
}

pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                sh 'echo Running build.'
            }
            post {
                always {
                influxDbPublisher(selectedTarget: 'jenkins')
              }
            }
        }
        stage('test') {
            steps {
                sh 'echo Running test.'
            }
            post {
              always {
                influxDbPublisher(selectedTarget: 'jenkins')
              }
            }
        }
    }
    post {
      always {
        influxDbPublisher(selectedTarget: 'jenkins')
      }
    }
}

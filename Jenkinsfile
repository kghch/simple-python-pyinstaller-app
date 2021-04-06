pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                sh 'echo Running build.'
            }
        }
        stage('test') {
            steps {
                sh 'echo Running test.'
            }
        }
    }
    post {
      always {
        influxDbPublisher(selectedTarget: 'jenkins')
      }
    }
}

pipeline {
    agent none
    stages {
        stage('Build') {
            agent {
                docker {
                    image 'python:2-alpine'
                }
            }
            steps {
                sh 'python -m py_compile sources/add2vals.py sources/calc.py'
            }
        }
        stage('Test') {
            agent {
                docker {
                    image 'qnib/pytest'
                }
            }
            steps {
                sh 'py.test --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
            }
            post {
                always {
                    junit 'test-reports/results.xml'
                }
            }
        }
    }
    post {
        always {
            def influxdb = Jenkins.instance.getDescriptorByType(jenkinsci.plugins.influxdb.InfluxDbStep.DescriptorImpl)
            def target = new jenkinsci.plugins.influxdb.models.Target()

            target.description = 'my-new-target'
            target.url = 'http://localhost:8086'

            target.username = 'admin'
            target.password = hudson.util.Secret.fromString('admin')

            target.database = 'jenkins'

            influxdb.addTarget(target)
            influxdb.save()

            influxDbPublisher(selectedTarget: 'my-new-target')
        }
    }
}

import io.jenkins.blueocean.rest.impl.pipeline.PipelineNodeGraphVisitor
import io.jenkins.blueocean.rest.impl.pipeline.FlowNodeWrapper
import org.jenkinsci.plugins.workflow.actions.TimingAction

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
            script {

                def visitor = new PipelineNodeGraphVisitor( currentBuild.rawBuild )

                // To find branches instead, replace NodeType.STAGE by NodeType.PARALLEL
                def stages = visitor.pipelineNodes.findAll{ it.type == FlowNodeWrapper.NodeType.STAGE }
                
                def myFields = [:]

                for( stage in stages ) {
                    if( stage.node.endNode ) {   // only finished stages have endNode
                        def startTime  = TimingAction.getStartTime( stage.node )
                        def endTime    = TimingAction.getStartTime( stage.node.endNode )
                        def duration   = endTime - startTime

                        myFields[stage.displayName] = duration
                        echo "Stage $stage.displayName duration: $duration ms" 
                    }
                } 

                influxDbPublisher(selectedTarget: 'jenkins', measurementName: 'total_table', customData: myFields)
            }
        }
    }
}

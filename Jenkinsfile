@Library('keptn-library@5.0')_
def keptn = new sh.keptn.Keptn()

node {
    properties([
        parameters([
         string(defaultValue: 'stage', description: 'Stage of your Keptn project where tests are triggered in', name: 'stage', trim: false), 
         string(defaultValue: '', description: 'Keptn Context ID', name: 'shkeptncontext', trim: false), 
         string(defaultValue: '', description: 'Triggered ID', name: 'triggeredid', trim: false), 
        ])
    ])

    def commit_id

    stage('Preparation') {
        checkout scm
    }

    stage('Initialize Keptn') {
        keptn.keptnInit project:"sockshop", service:"carts", stage:"${params.stage}"
    }

    stage('Test') {
        // Run your tests here
    }

    stage('Send Finished Event Back to Keptn') {
        // Send test.finished Event back
        def keptnContext = keptn.sendFinishedEvent eventType: "test", keptnContext: "${params.shkeptncontext}", triggeredId: "${params.triggeredid}", result:"pass", status:"succeeded", message:"jenkins tests succeeded"
        String keptn_bridge = env.KEPTN_BRIDGE
        echo "Open Keptns Bridge: ${keptn_bridge}/trace/${keptnContext}"
    }
}

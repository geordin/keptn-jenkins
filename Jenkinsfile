@Library('keptn-library@6.0.0')
import sh.keptn.Keptn
def keptn = new sh.keptn.Keptn()



node {
  stage('Trigger Delivery') {
  keptn.keptnInit project:"sockshop", service:"carts", stage:"dev"
  echo "Progressive Delivery: Triggering Keptn to deliver ${params.Image}"
  
  def keptnContext = keptn.sendDeliveryTriggeredEvent image:"docker.io/keptnexamples/carts:0.13.3"
  String keptn_bridge = env.KEPTN_BRIDGE
  echo "Open Keptns Bridge: ${keptn_bridge}/trace/${keptnContext}"
  
  }
  stage('Wait for Result') {
        waitTime = 0
        if(params.WaitForResult?.isInteger()) {
            waitTime = params.WaitForResult.toInteger()
        }

        if(waitTime > 0) {
            echo "Waiting until Keptn is done and returns the results"
            def result = keptn.waitForEvaluationDoneEvent setBuildResult:true, waitTime:60
            echo "${result}"
        } else {
            echo "Not waiting for results. Please check the Keptns bridge for the details!"
        }
    }
}

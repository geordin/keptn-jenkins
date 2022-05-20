@Library('keptn-library@6.0.0')
import sh.keptn.Keptn
def keptn = new sh.keptn.Keptn()


// Initialize Keptn: "Link" it to your Jenkins Pipeline
// -------------------------------------------
// initialize keptn: will store project, service and stage in a local context file so you don't have to pass it to all other functions
//
// ⚠⚠⚠ keptn.keptnInit function is deprecated and will stop working once Keptn requires a git upstream repo when creating a project.
// It is recommended to use the Keptn CLI/API for project creation.
keptn.keptnInit project:"sockshop", service:"carts", stage:"dev"

def keptnContext = keptn.sendDeliveryTriggeredEvent image:"docker.io/keptnexamples/carts:0.13.3"
String keptn_bridge = env.KEPTN_BRIDGE
echo "Open Keptns Bridge: ${keptn_bridge}/trace/${keptnContext}"

// --------------------------------------------
// Waiting for Quality Gate Result (5 Minutes)
// --------------------------------------------
def result = keptn.waitForEvaluationDoneEvent setBuildResult:true, waitTime:5
echo "${result}"

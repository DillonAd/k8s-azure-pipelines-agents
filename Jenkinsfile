stage("Deploy") {
    timeout(time: 7, unit: "DAYS") {
        input(message: "Deploy?", ok: "Make it so.")
        input(message: "This can drop agents currently building projects. Are you sure?", ok: "Sure I\'m sure")
    }
    node {
        checkout scm

        def deploymentExists = sh(script: "kubectl describe replicationController/vsts-agent", returnStatus: true)

        if(deploymentExists == 0) {
            sh "kubectl delete replicationController vsts-agent"
        }
        
        sh "kubectl create -f ${WORKSPACE}/deploy.yaml"
    }
}
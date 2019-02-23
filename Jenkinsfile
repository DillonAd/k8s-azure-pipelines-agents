stage("Deploy") {
    timeout(time: 7, unit: "DAYS") {
        input(message: "Deploy?", ok: "Make it so.")
        input(message: "This can drop agents currently building projects. Are you sure?", ok: "Sure I\'m sure")
    }

    node {
        var deploymentExists = sh("kubectl describe replicationController/vsts-agent", returnStatus: true)

        if(deploymentExists) {
            sh "kubectl rolling-update vsts-agent -f deploy.yaml"
        } else {
            sh "kubectl create -f deploy.yaml"
        }
    }
}
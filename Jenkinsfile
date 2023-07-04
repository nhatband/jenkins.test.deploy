node_label = params.node_label ? params.node_label : env.node_label
node(node_label) {
        checkout scm
        env.DOCKER_API_VERSION="1.23"

        sh "git rev-parse --short HEAD > commit-id"
        tag = readFile('commit-id').replace("\n", "").replace("\r", "")
        registry_host = env.registry_host

        // build
        stage("build: jenkins-test-deploy"){
            sh "docker build --tag nhatdev/jenkins.test.deploy:latest --file Dockerfile ."
        }

        // push
        stage("push"){
            sh "docker push nhatdev/jenkins.test.deploy:latest"
        }

        // deploy
        stage("deploy"){
            sh "sed -i 's|{{tag}}|${tag}|g' deployment.yaml \
            && sed -i 's|{{registry_host}}|${registry_host}|g' deployment.yaml \
            && kubectl ${env.token_kube} apply -f deployment.yaml"
        }
}
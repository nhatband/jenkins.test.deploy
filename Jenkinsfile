node_label = params.node_label ? params.node_label : env.node_label
node(node_label) {
        checkout scm
        env.DOCKER_API_VERSION="1.23"

        bat "git rev-parse --short HEAD > commit-id"
        tag = readFile('commit-id').replace("\n", "").replace("\r", "")
        registry_host = env.registry_host

        // build
        stage("build: jenkins-test-deploy"){
            bat "docker build --tag nhatdev/jenkins.test.deploy:latest --file Dockerfile ."
        }


        // deploy
        stage("deploy"){
            bat "kubectl apply -f deployment.yaml"
        }
}
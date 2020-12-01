node {
    def app
    stage('Clone Repository') {
        checkout scm
    }

    stage('Build Image') {
        app = docker.build("lovetwocode/react-docker-jenkins")
    }

    stage('Test Image') {
        app.inside {
            echo "Test passed"
        }
    }

    stage('Push Image') {
        withDockerRegistry([ credentialsId: "docker-hub", url: "" ]) {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
        // docker.withRegistry("https://hub.docker.com", "docker-hub") {
        //     app.push("${env.BUILD_NUMBER}")
        //     app.push("latest")
        // }
        echo "Trying to push docker build to dockerhub"
    }
}
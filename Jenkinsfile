node {
    def app

    stage('Clone') {
        checkout scm
    }

    stage('Build image') {
        app = docker.build("localhost:5000/nginx-aziz")
    }

    stage('Push image') {
        docker.withRegistry('http://localhost:5000') {
            app.push("latest")
        }
    }

    stage('Run image') {
        docker.image('localhost:5000/nginx-aziz').withRun('-p 8090:80') { c ->
            sh 'docker ps'
            sh 'curl localhost:8090'
        }
    }
}

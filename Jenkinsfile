node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Build image') {
        app = docker.build("saberdocker/liberty:latest")
    }

    stage('Test image') {
        app.inside {
             sh 'echo "Tests passed" '
        }
    }
 
    stage('Push image') {
       docker.withRegistry('https://registry.hub.docker.com', 'jenkinshub') {
         app.push("${env.BUILD_NUMBER}")
         app.push("latest")
       }
   }
}


node {
    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        git url: 'https://github.com/gauthamdharsan/JenkinsNodejs-Docker-pipeline.git'
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

        app = docker.build("gauthamdharsan/nodejsstarter")
    }

    //stage('Test image') {
    //    /* Ideally, we would run a test framework against our image.
     //    * For this example, we're using a Volkswagen-type approach ;-) */

        //app.inside {
          //  sh 'echo "Tests passed"'
        //}
    //}
    
    stage('sonar-scanner') {
        withCredentials([string(credentialsId: 'sonar')]) {
        sh "${sonarqubeScannerHome}/bin/sonar-scanner -e -Dsonar.host.url=http://localhost:9000 -Dsonar.login=${sonarLogin} -Dsonar.projectName=nodejsstarter -Dsonar.projectVersion=${env.BUILD_NUMBER} -Dsonar.projectKey=sonar -Dsonar.sources=complete/src/main/ -Dsonar.tests=complete/src/test/ -Dsonar.language=java -Dsonar.java.binaries=."
      }
    }  
    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
        docker.withRegistry('https://registry.hub.docker.com', 'docker') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}

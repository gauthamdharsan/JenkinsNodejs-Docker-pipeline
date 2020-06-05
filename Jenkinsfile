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
    
    stage('sonarqube analysis') {
        def sonarqubeScannerHome = tool name: 'sonarqube'
          
    }  
    stage('Push image') {
        
        docker.withRegistry('https://registry.hub.docker.com', 'docker') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}

pipeline {
    agent any;

    stages {

        stage("Code") {
            steps {
                echo "Code clone start"
                git url:"https://github.com/nitishgarg1/two-tier-flask-app.git/",branch:"master"
                echo "code clone end"
            }
        }

        stage("Build") {
            steps {
                echo "Build start ho gaya"
                sh "docker build -t myapp:latest ."
                echo "Build end ho gaya"
            }
        }

        stage("push to dockerhub") {
            steps {
               withCredentials([usernamePassword(
                   credentialsId: 'dockerHubCreds', 
                    usernameVariable: 'USER', 
                   passwordVariable: 'PASS'
             )]) {
                    sh "docker login -u ${env.USER} -p ${env.PASS}"
                    sh "docker image tag myapp:latest ${env.USER}/flaskapp:latest"
                    sh "docker push ${env.USER}/flaskapp:latest"
            }
          
            }
        }

        stage("Deploy") {
            steps {
                echo "Deploy start ho gaya"
                sh "docker compose up -d "
                 echo "Deploy end ho gaya"
            }
        }
    }
}

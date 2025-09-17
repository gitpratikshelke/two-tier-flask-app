// pipeline{
//     agent any;
//     stages{
//         stage("code clone"){
//             steps{
//                 git url: "https://github.com/gitpratikshelke/two-tier-flask-app.git", branch: "master"
//             }
//         }
//         stage("build"){
//             steps{
//                 sh "docker build -t  two-tier-flask-app ."
//             }
//         }
//         stage("test"){
//             steps{
//                 echo "test go gya"
//             }
//         }
//         stage("push to docker"){
//             steps{
//                 withCredentials([usernamePassword(
//                     credentialsId:"dockerHubCreds",
//                     passwordVariable: "dockerHubPass",
//                     usernameVariable: "dockerHubUser"
//                 )]){
//                 sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
//                 sh "docker image tag two-tier-flask-app ${env.dockerHubUser}/two-tier-flask-app"
//                 sh "docker push ${env.dockerHubUser}/two-tier-flask-app:latest"
//             }
//        }
//        }
        
//          stage("deploy"){
//             steps{
//                 sh "docker compose up -d --build flask-app"
//             }
//         }
//     }
// }


pipeline {
    agent any
    stages {
        stage("code clone") {
            steps {
                git url: "https://github.com/gitpratikshelke/two-tier-flask-app.git", branch: "master"
            }
        }

        stage("build & push to docker") {
            steps {
                withDockerRegistry([credentialsId: 'dockerHubCreds', url: '']) {
                    sh "docker build -t ${env.dockerHubUser}/two-tier-flask-app:latest ."
                    sh "docker push ${env.dockerHubUser}/two-tier-flask-app:latest"
                }
            }
        }

        stage("test") {
            steps {
                echo "test go gya"
            }
        }

        stage("deploy") {
            steps {
                // Adjust if using docker-compose instead of docker compose
                sh "docker compose up -d --build flask-app"
            }
        }
    }
}



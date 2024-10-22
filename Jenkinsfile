pipeline {
    agent any 
    stages {
        
        stage ("Git checkout") {
            steps {
                git branch: 'main', url: 'https://github.com/RevanthReddyCh/starbucks.git'
            }
        }
       
       
        stage("Install NPM Dependencies") {
            steps {
                sh "npm install"
            }
        }
       
        stage ("Build Docker Image") {
            steps {
                sh "docker build -t starbucks ."
            }
        }
        // stage ("Tag & Push to DockerHub") {
        //     steps {
        //         script {
        //             withDockerRegistry(credentialsId: 'docker') {
        //                 sh "docker tag starbucks amonkincloud/starbucks:latest "
        //                 sh "docker push amonkincloud/starbucks:latest "
        //             }
        //         }
        //     }
        // }
        // stage('Docker Scout Image') {
        //     steps {
        //         script{
        //            withDockerRegistry(credentialsId: 'docker', toolName: 'docker'){
        //                sh 'docker-scout quickview amonkincloud/starbucks:latest'
        //                sh 'docker-scout cves amonkincloud/starbucks:latest'
        //                sh 'docker-scout recommendations amonkincloud/starbucks:latest'
        //            }
        //         }
        //     }
        // }
        stage ("Deploy to Conatiner") {
            steps {
                sh 'docker rm -f '
                sh 'docker run -d --name starbucks -p 80:3000 starbucks'
            }
        }
    }
    // post {
    // always {
    //     emailext attachLog: true,
    //         subject: "'${currentBuild.result}'",
    //         body: """
    //             <html>
    //             <body>
    //                 <div style="background-color: #FFA07A; padding: 10px; margin-bottom: 10px;">
    //                     <p style="color: white; font-weight: bold;">Project: ${env.JOB_NAME}</p>
    //                 </div>
    //                 <div style="background-color: #90EE90; padding: 10px; margin-bottom: 10px;">
    //                     <p style="color: white; font-weight: bold;">Build Number: ${env.BUILD_NUMBER}</p>
    //                 </div>
    //                 <div style="background-color: #87CEEB; padding: 10px; margin-bottom: 10px;">
    //                     <p style="color: white; font-weight: bold;">URL: ${env.BUILD_URL}</p>
    //                 </div>
    //             </body>
    //             </html>
    //         """,
    //         to: 'provide_your_Email_id_here',
    //         mimeType: 'text/html',
    //         attachmentsPattern: 'trivy.txt'
    //     }
    // }
}

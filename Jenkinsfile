pipeline {
    agent any
    stages{
        stage('git cloned'){
            steps{
                git url:'https://github.com/LOKESH-creator660/php-project-CI-CD/', branch: "master"
              
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t lokil5762049/2febimg:v1 .'
                    sh 'docker images'
                }
            }
        }
          stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd-loki', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push lokil5762049/2febimg:v1'
                }
            }
        }
        
     stage('Deploy') {
            steps {
               script {
                   def dockerrm = 'sudo docker rm -f My-first-containe221 || true'
                    def dockerCmd = 'sudo docker run -itd --name My-first-containe221 -p 8083:80 lokil5762049/2febimg:v1'
                    sshagent(['sshkeypair']) {
                        //chnage the private ip in below code
                        // sh "docker run -itd --name My-first-containe211 -p 8083:80 lokil5762049/2febimg:v1"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.47.230 ${dockerrm}"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.47.230 ${dockerCmd}"
                    }
                }
            }
        }
    }
}

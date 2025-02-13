node {
    stage('Checkout') {
        git branch: 'react-app', url: 'https://github.com/daffaverse/a428-cicd-labs.git'
    }
    
    docker.image('node:16-buster-slim').inside {
        stage('Build') {
            sh 'npm install'
            sh 'npm run build'
        }
        
        stage('Test') {
            sh 'npm test'
        }
        
        stage('Manual Approval') {
            input message: 'Lanjutkan ke tahap Deploy?'
        }
        
        stage('Deploy') {
             sshagent(['gcp-ssh-key']) {
                 sh """
                    scp -o StrictHostKeyChecking=no -r build/* c312b4ky1672@34.29.4.55:/home/c312b4ky1672/app
                    ssh -o StrictHostKeyChecking=no c312b4ky1672@34.29.4.55 'cd ~/app && npm install && pm2 restart app || pm2 start npm --name app -- start'
                """
                sleep 60
            }
        }
    }
}

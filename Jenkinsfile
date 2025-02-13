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
            withCredentials([sshUserPrivateKey(credentialsId: 'gcp-ssh-key', keyFileVariable: 'SSH_KEY')]) {
                sh """
                    scp -i \$SSH_KEY -o StrictHostKeyChecking=no dist/add2vals c312b4ky1672@34.143.130.225:/home/c312b4ky1672/python-app/
                    ssh -i \$SSH_KEY -o StrictHostKeyChecking=no c312b4ky1672@34.143.130.225 'chmod +x ~/python-app/add2vals'
                """
                sleep 60
            }
        }
    }
}

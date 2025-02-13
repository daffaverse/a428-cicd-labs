node {
    stage('Checkout') {
        git branch: 'react-app', url: 'https://github.com/daffaverse/a428-cicd-labs.git'
    }
    
    docker.image('node:16-buster-slim').inside('--network host') {
        stage('Build') {
            sh 'npm install'
            sh 'npm run build'
        }
        
        stage('Test') {
            sh 'npm test'
        }
    }
    
    stage('Manual Approval') {
        sh './jenkins/scripts/deliver.sh' 
        input message: 'Lanjutkan ke tahap Deploy?'
    }
    
    stage('Deploy') {
        sshagent(credentials: ['gcp-ssh-key']) {
            sh """
                scp -o StrictHostKeyChecking=no -r package.json build/* c312b4ky1672@35.223.229.24:/home/c312b4ky1672/app/
            """
        }

        echo 'Apliaksi berhasil di Deploy'
        sleep time: 60, unit: 'SECONDS'
    }
}

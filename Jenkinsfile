node {
    stage('Checkout') {
        git branch: 'react-app', url: 'https://github.com/daffaverse/a428-cicd-labs.git'
    }
    
    docker.image('node:16-buster-slim').inside {
        stage('Build') {
            sh 'npm install'
        }
        
        stage('Test') {
            sh 'npm test'
        }

        stage('Deploy') {
            sh './jenkins/scripts/deliver.sh'
            input massage: 'Sudah selesai menggunakan react app? (klik "end")'
            sh './jenkins/script/kill.sh'
        }
    }
}

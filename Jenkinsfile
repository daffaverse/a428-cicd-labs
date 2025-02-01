node {
    stage('checkout') {
        git branch: 'react-app', url: 'https://github.com/daffaverse/a428-cicd-labs.git'
    }
    stage('Build') {
        sh 'npm install'
    }
    stage('Test') {
        sh 'npm test'
    }
}
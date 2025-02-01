node {
    stage('checkout') {
        git branch: 'react-app', url: 'https://github.com/daffaverse/a428-cicd-labs.git'
    }
    stage('Install') {
        sh 'npm install'
    }
    stage('Test') {
        sh 'npm test'
    }
}
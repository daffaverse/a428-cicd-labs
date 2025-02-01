node {
    stage('Checkout') {
        git branch: 'react-app', url: '[URL repository Anda]'
    }
    
    stage('Install') {
        sh 'npm install'
    }
    
    stage('Test') {
        sh 'npm test'
    }
}
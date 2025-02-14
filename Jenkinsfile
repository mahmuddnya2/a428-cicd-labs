node {
    docker.image('node:16-buster-slim').inside('-p 3000:3000') {
        stage('Build') {
            sh 'npm install'
        }
        stage('Test') {
            sh './jenkins/scripts/test.sh'
            input message: 'Lanjut ke tahap Deploy? (Click "Proceed" to continue)'
        }
        stage('Deploy'){
            sh './jenkins/scripts/deliver.sh' 
            sleep(60)
            sh './jenkins/scripts/kill.sh' 
        }
    }
}

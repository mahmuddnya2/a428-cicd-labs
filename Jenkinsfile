node {
    docker.image('node:16-buster-slim').inside('-p 3000:3000') {
        stage('Build') {
            sh 'npm install'
        }
        stage('Test') {
            sh './jenkins/scripts/test.sh'
            input message: 'Finished using the website?'
            script {
            choice = input(id: 'my-choice', message: 'Finished using the website? (Click "Proceed" to continue)', choices: ['Proceed', 'Abort'], submitter: { choice ->
                if (choice == 'Abort') {
                    error 'Process aborted by user'
                }
            })
        }
        }
        stage('Deploy'){
            sh './jenkins/scripts/deliver.sh' 
            sleep(10)
            sh './jenkins/scripts/kill.sh' 
        }
    }
}

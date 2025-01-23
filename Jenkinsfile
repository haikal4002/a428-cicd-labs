node {
    checkout scm
    docker.image('node:16-buster-slim').inside('-p 3000:3000') {
        stage('Build') {
            sh 'npm install'
        }
        stage('Test') {
            sh './jenkins/scripts/test.sh'
        }
        stage('Manual Approval'){
            input message: 'Lanjutkan ke tahap Deploy?'
        }
        stage('Deploy'){
            sh './jenkins/scripts/deliver.sh'
            echo 'Aplikasi react app berhasil di deploy'
            input message: 'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)'
            sh './jenkins/scripts/kill.sh'
        }
        echo "Sleep for 1 minute"
        sleep time: 60, unit: "SECONDS"
        
    }
}

node {
    def dockerImage = docker.image('node:lts-buster-slim')
    dockerImage.inside('-p 3000:3000') {
        env.CI = 'true'
        stage('Build') {
            sh 'npm install'
        }
        stage('Test') {
            sh './jenkins/scripts/test.sh'
        }
        stage('Manual Approval') {
            input message: 'Lanjutkan ke tahap Deploy? (Klik "Proceed" untuk melanjutkan eksekusi pipeline ke tahap Deploy atau klik "Abort" untuk menghentikan eksekusi pipeline)',
                  ok: 'Proceed'
        }
        stage('Deploy') {
            sh './jenkins/scripts/deliver.sh'
            echo 'Aplikasi berjalan selama 1 menit...'
            sleep 60
            sh './jenkins/scripts/kill.sh'
        }
    }
}

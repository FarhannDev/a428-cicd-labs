// Menggunakan scripted pipeline

node {
    stage('Build') {
        checkout scm
        docker.image('node:16-buster-slim').inside('-p 3000:3000') {
            sh 'npm install'
        }
    }

    stage('Test') {
        checkout scm
        docker.image('node:16-buster-slim').inside('-p 3000:3000') {
            sh './jenkins/scripts/test.sh'
        }
    }

    stage('Manual Approval') {
        // Meminta input dari pengguna
        timeout(time: 7, unit: 'DAYS') {
            def userInput = input message: 'Lanjutkan ke tahap Deploy?',
                                  parameters: [
                                      choice(name: 'ACTION', choices: ['Proceed', 'Abort'], description: 'Pilih "Proceed" untuk melanjutkan atau "Abort" untuk membatalkan.')
                                  ]
            if (userInput == 'Abort') {
                error('Pipeline dihentikan oleh pengguna.')
            }
        }
    }

    stage('Deploy') {
        checkout scm
        docker.image('node:16-buster-slim').inside('-p 3000:3000') {
            // Langkah-langkah untuk melakukan deployment
            sh './jenkins/scripts/deliver.sh' 
            input message: 'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)'
            // Menjalankan perintah sleep untuk menjeda eksekusi selama 1 menit
            sh 'sleep 60'
            // Eksekusi Pipeline pada Deploy Stage
            sh './jenkins/scripts/kill.sh' 
        }
    }
}

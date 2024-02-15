// Menggunakan Scripted Pipeline
node {
    // Menggunakan Docker sebagai agent untuk menjalankan langkah-langkah
    docker.image('node:16-buster-slim').withRun('-p 3000:3000') {
        // Tahap untuk membangun proyek
        stage('Build') {
            sh 'npm install'
        }
        // Tahap untuk menjalankan tes
        stage('Test') {
            sh './jenkins/scripts/test.sh'
        }
    }
}
// Menggunakan Scripted Pipeline
node {
    // Menggunakan Docker sebagai agent untuk menjalankan langkah-langkah
    docker.image('node:16-buster-slim').withRun('-p 3000:3000') {
        // Tahap untuk membangun proyek
        stage('Build') {
            steps {
                sh 'apt-get update && apt-get install -y nodejs npm'
             }
        }
        // Tahap untuk menjalankan tes
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
           
        }
    }
}

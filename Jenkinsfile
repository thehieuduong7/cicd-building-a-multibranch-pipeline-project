pipeline {
    agent { label 'ubuntu-10.6.5.21' }

    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
                // withCredentials([string(credentialsId: 'sudo-vm21-password', variable: 'SUDO_PASS')]) {
                //     sh 'sudo -S npm install'
                // }
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                // sh './jenkins/scripts/test.sh'
                echo 'test success!'
            }
        }
        stage('Deliver for development') {
            when {
                branch 'development'
            }
            steps {
                sh './jenkins/scripts/deliver-for-development.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
        stage('Deploy for production') {
            when {
                branch 'production'
            }
            steps {
                sh './jenkins/scripts/deploy-for-production.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}

pipeline {
    agent any
    stages {
        stage('Print Output 1') {
            steps { 
                echo 'Hallo devtian'
            }
        }
        stage('Print Output 2') {
            steps { 
                sh'''
                pwd && whoami && echo "Test Pipeline"
                '''
            }
        }
    }
}
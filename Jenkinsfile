pipeline {
    agent any

    environment {
        M2_HOME = '/usr/share/maven'
        PATH = "${M2_HOME}/bin:${PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[url: 'https://github.com/Oussemabdellaoui/atelierDevops-merge']]
                ])
            }
        }

        stage('Build') {
            steps {
                sh 'ls -la'  // Verify project is cloned
                sh 'mvn clean compile'
            }
        }

        stage('Deploy to Nexus') {
            steps {
                // Use withCredentials to inject Nexus username and password
                withCredentials([usernamePassword(credentialsId: 'nexus-credentials', 
                                                 usernameVariable: 'admin', 
                                                 passwordVariable: 'Ouss8922.1!')]) {
                    sh 'mvn deploy -DskipTests=true -Dusername=$admin -Dpassword=$Ouss8922.1!'
                }
            }
        }
    }
}

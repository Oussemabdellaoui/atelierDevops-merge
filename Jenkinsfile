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
                sh 'mvn deploy -DaltDeploymentRepository=deploymentRepo::default::http://192.167.33.10:8083/repository/maven-releases/'
            }
        }
    }
}

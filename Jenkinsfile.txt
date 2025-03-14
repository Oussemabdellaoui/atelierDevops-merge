pipeline {
    agent any

    environment {
        M2_HOME = '/usr/share/maven'
        PATH = "${M2_HOME}/bin:${PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                sh 'git --version'
                sh 'git ls-remote https://github.com/Oussemabdellaoui/atelierDevops-merge'
                git branch: 'main', url: 'https://github.com/Oussemabdellaoui/atelierDevops-merge'
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

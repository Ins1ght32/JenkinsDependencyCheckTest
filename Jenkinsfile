pipeline {
    agent any
    environment {
        NVD_API_KEY = credentials('7ad48849-c21a-49f4-9ddb-85151d39d039')
    }
    stages {
        stage('Checkout SCM') {
            steps {
                git '/home/JenkinsDependencyCheckTest'
            }
        }

        stage('OWASP DependencyCheck') {
            steps {
                dependencyCheck additionalArguments: '--nvd-apiKey $NVD_API_KEY --format HTML --format XML', odcInstallation: 'Default'
            }
        }
    }    
    post {
        success {
            dependencyCheckPublisher pattern: 'dependency-check-report.xml'
        }
    }
}

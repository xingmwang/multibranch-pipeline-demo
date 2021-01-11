pipeline {

    agent {
        node {
            label 'master'
        }
    }

    stages {

        stage('Cleanup Workspace') {
            steps {
                cleanWs()
                try {
                    timeout(time: 5,unit: 'SECONDS') {
                        build job: 'simple-pipline-test/develop', parameters: [ string(name: 'ENVIRONMENT_TAG', value: 'cap'),string(name: 'FORCE_RUN', value: 'yes')]
                    }
                } catch (Exception e) {
                    echo "downstream job run false"
                }
            }
        }

        stage(' Unit Testing') {
            steps {
                sh """
                echo "Running Unit Tests"
                """
            }
        }

        stage('Code Analysis') {
            steps {
                sh """
                echo "Running Code Analysis"
                """
            }
        }

        stage('Build Deploy Code') {
            when {
                branch 'develop'
            }
            steps {
                sh """
                echo "Building Artifact"
                """

                sh """
                echo "Deploying Code"
                """
            }
        }

    }
}

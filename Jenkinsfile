pipeline {
    agent any

    parameters {
        booleanParam(name: 'build', defaultValue: true, description: 'Check for running build stage')
        booleanParam(name: 'sonar', defaultValue: true, description: 'Check for running sonar stage')
        booleanParam(name: 'test', defaultValue: true, description: 'Check for running test stage')
    }

    stages {
        stage('build') {
            steps {
                sh 'echo "This is build stage"'
            }
        }

        stage('sonar') {
            steps {
                sh 'echo "This is sonar stage"'
            }
        }

        stage('test') {
            steps {
                sh 'echo "This is test stage"'
            }
        }
    }

}
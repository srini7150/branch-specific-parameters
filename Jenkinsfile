pipeline {
    agent any

    parameters {
        booleanParam(name: 'build', defaultValue: true, description: 'Check for running build stage (Not applicable for feature branches)')
        booleanParam(name: 'sonar', defaultValue: true, description: 'Check for running sonar stage (Not applicable for feature branches)')
        booleanParam(name: 'test', defaultValue: true, description: 'Check for running test stage (Not applicable for feature branches)')
    }

    stages {
        stage('build') {
            when {
                expression {
                    params.build || isFeatureBranch()
                }
            }
            steps {
                sh 'echo "This is build stage"'
            }
        }

        stage('sonar') {
            when {
                expression {
                    params.sonar || isFeatureBranch()
                }
            }
            steps {
                sh 'echo "This is sonar stage"'
            }
        }

        stage('test') {
            when {
                expression {
                    params.test || isFeatureBranch()
                }
            }
            steps {
                sh 'echo "This is test stage"'
            }
        }
    }

}

def isFeatureBranch() {
    return env.BRANCH_NAME.startsWith('feature')
}
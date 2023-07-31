pipeline {
    agent any

    parameters {
        booleanParam(name: 'build', defaultValue: true, description: 'Check for running build stage (Not applicable for feature branches)')
        booleanParam(name: 'sonar', defaultValue: true, description: 'Check for running sonar stage (Not applicable for feature branches)')
        booleanParam(name: 'test', defaultValue: true, description: 'Check for running test stage (Not applicable for feature branches)')
    }

    options {
        buildDiscarder logRotator(numToKeepStr: '5')
    }

    stages {
        stage('build') {
            when {
                expression {
                    params.build || BRANCH_NAME =~ /^feature/
                }
            }
            steps {
                sh 'echo "This is build stage"'
            }
        }

        stage('sonar') {
            when {
                expression {
                    params.sonar || BRANCH_NAME =~ /^feature/
                }
            }
            steps {
                sh 'echo "This is sonar stage"'
            }
        }

        stage('test') {
            when {
                expression {
                    params.test || BRANCH_NAME =~ /^feature/
                }
            }
            steps {
                sh 'echo "This is test stage"'
            }
        }

        stage('hotfix or release') {
            when {
                expression {
                    BRANCH_NAME == "release" || BRANCH_NAME =~ /(hotfix.*)/
                }
            }
            steps {
                sh 'echo "This is hotfix or release branch"'
                sh "echo 'branch_name is: ${BRANCH_NAME}'"
            }
        }

    }

}

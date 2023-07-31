pipeline {
    agent any

    environment {
        VERSION = ""
        SUB_MINOR_VERSION = ""
        INIT_RELEASE_BUILD_NO = ""
    }

    parameters {
        booleanParam(name: 'build', defaultValue: true, description: 'Check for running build stage (Not applicable for feature branches)')
        booleanParam(name: 'sonar', defaultValue: true, description: 'Check for running sonar stage (Not applicable for feature branches)')
        booleanParam(name: 'test', defaultValue: true, description: 'Check for running test stage (Not applicable for feature branches)')
    }

    options {
        buildDiscarder logRotator(numToKeepStr: '5')
    }

    stages {

        stage('versioning') {
            steps {
                script {
                    VERSION = readFile('versions/version.counter')
                    INIT_RELEASE_BUILD_NO = readFile('versions/init_release_build_no')
                    SUB_MINOR_VERSION = BUILD_NUMBER.toInteger() - INIT_RELEASE_BUILD_NO.toInteger()
                    VERSION = VERSION.split('\\.')
                    echo "VERSION[0] = ${VERSION[0]}"
                    echo "VERSION[1] = ${VERSION[1]}"
                    echo "VERSION[2] = ${VERSION[2]}"
                    echo "updating VERSION[2] to sub minor version"
                    VERSION[2] = SUB_MINOR_VERSION
                    echo "updated VERSION[2] to sub minor version is: ${VERSION[2]}"
                    VERSION = VERSION[0] + "." + VERSION[1] + "." + VERSION[2]
                    echo "Updated version is ${VERSION}"
                }
            }
        }

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


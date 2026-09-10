pipeline {
    agent any

    options {
        ansiColor('xterm')
    }

    stages {
        stage('build') {
            steps {
                bat 'npm ci'
                bat 'npm run build'
            }
        }

        stage('test') {
            parallel {
                stage('unit tests') {
                    steps {
                        // Unit tests with Vitest
                        bat 'npx vitest run --reporter=verbose'
                    }
                }
            }
        }

        stage('deploy') {
            steps {
                // Mock deployment which does nothing
                echo 'Mock deployment was successful!'
            }
        }
    }
}
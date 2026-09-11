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

                stage('integration test') {
                    steps {
                        bat 'npx playwright install'
                        bat 'npx playwright test --project=chromium'
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
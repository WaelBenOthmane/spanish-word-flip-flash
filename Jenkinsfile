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

        stage('e2e') {
            environment {
                E2E_BASE_URL = 'https://spanish-cards.netlify.app/'
            }
            steps {
                bat 'npx playwright test --project=chromium'
            }

            post {
                always{
                    publishHTML([allowMissing: false, alwaysLinkToLastBuild: true, icon: '', keepAll: false, reportDir: 'reports-e2e/html/', reportFiles: 'index.html', reportName: 'Playwright HTML Report', reportTitles: '', useWrapperFileDirectly: true])
                    junit stdioRetention: 'ALL', testResults: 'reports-e2e/junit.xml'
                }
            }
            
        }
    }
}
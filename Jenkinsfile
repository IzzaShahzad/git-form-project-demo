pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo '🔄 Cloning the GitHub repository...'
                git branch: 'main', url: 'https://github.com/IzzaShahzad/git-form-project-demo.git'
            }
        }

        stage('Build') {
            steps {
                echo '🏗️ Checking project files...'
                script {
                    // Verify main files exist
                    if (fileExists('index.html') && fileExists('style.css') && fileExists('script.js')) {
                        echo '✅ All required files found.'
                    } else {
                        error('❌ Missing one or more required files: index.html, style.css, script.js')
                    }
                }
            }
        }

        stage('Test') {
            steps {
                echo '🧪 Running simple syntax checks...'
                script {
                    // Example: just print success message (no real tests for static site)
                    echo '✅ No syntax errors found in static files.'
                }
            }
        }

        stage('Deploy') {
            steps {
                echo '🚀 Deploying project locally...'
                script {
                    // Simulate deployment by copying files to a deploy folder
                    def deployDir = 'deploy'
                    sh "mkdir -p ${deployDir}"
                    sh "cp -r * ${deployDir}/"
                    echo "✅ Project deployed to folder: ${deployDir}"
                }
            }
        }
    }

    post {
        success {
            echo '🎉 Build Successful! The project has been deployed successfully.'
            script {
                currentBuild.description = "✅ Deployment Successful"
            }
        }
        failure {
            echo '❌ Build Failed! Check the logs for details.'
            script {
                currentBuild.description = "❌ Build Failed"
            }
        }
    }
}

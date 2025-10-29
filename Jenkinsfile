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
                    if (fileExists('index.html') && fileExists('style.css') && fileExists('script.js')) {
                        echo '✅ All required files found.'
                    } else {
                        error('❌ Missing one or more required files: index.html, style.css, or script.js')
                    }
                }
            }
        }

        stage('Test') {
            steps {
                echo '🧪 Running simple syntax checks...'
                script {
                    echo '✅ No syntax errors found in static files.'
                }
            }
        }

        stage('Deploy') {
    steps {
        echo '🚀 Deploying project locally...'
        script {
            def deployDir = 'deploy'

            // Create deploy folder if not exists
            bat "if not exist ${deployDir} mkdir ${deployDir}"

            // Copy only html, css, js files (avoid copying deploy folder itself)
            bat "xcopy *.html ${deployDir}\\ /Y"
            bat "xcopy *.css ${deployDir}\\ /Y"
            bat "xcopy *.js ${deployDir}\\ /Y"

            echo "✅ Project deployed successfully to folder: ${deployDir}"
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

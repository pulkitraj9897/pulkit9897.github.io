pipeline {
    agent any

    environment {
        LOCAL_PROJECT_DIR = '/var/local/flask-site'
        BRANCH_NAME = 'main'
        GITHUB_REPO = 'https://github.com/pulkitraj9897/pulkit9897.github.io.git'
    }

    stages {
        stage('Prepare Workspace') {
            steps {
                cleanWs()
            }
        }

        stage('Push Changes') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'devops', variable: 'GITHUB_TOKEN')]) {
                        sh """
                            # Create a clean temporary directory
                            TEMP_DIR=\$(mktemp -d)
                            
                            # Clone the repository into temp directory
                            git clone ${GITHUB_REPO} \$TEMP_DIR
                            
                            # Copy your local files to the cloned repository
                            cp -r ${LOCAL_PROJECT_DIR}/* \$TEMP_DIR/
                            
                            # Configure git
                            cd \$TEMP_DIR
                            git config user.email "pulkitraj9897@gmail.com"
                            git config user.name "pulkit9897"
                            
                            # Commit and push changes using the token
                            git add .
                            git commit -m "Automated commit ${BUILD_NUMBER}" || echo "No changes to commit"
                            git push https://\${GITHUB_TOKEN}@github.com/pulkitraj9897/pulkit9897.github.io.git ${BRANCH_NAME}
                            
                            # Clean up
                            cd ..
                            rm -rf \$TEMP_DIR
                        """
                    }
                }
            }
        }
    }

    post {
        success {
            echo '🚀 Pushed from local folder successfully!'
        }
        failure {
            echo '😓 Push failed, check your logs.'
        }
    }
}
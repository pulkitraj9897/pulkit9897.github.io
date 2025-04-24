pipeline {
    agent any
    
    environment {
        GITHUB_REPO = 'https://github.com/pulkit9897/pulkit9897.github.io.git'
        BRANCH_NAME = 'main'
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Configure Git') {
            steps {
                script {
                    sh '''
                        git config user.email "pulkitraj9897@gmail.com"
                        git config user.name "pulkit9897"
                    '''
                }
            }
        }
        
        stage('Commit and Push Changes') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'devops', variable: 'GITHUB_TOKEN')]) {
                        sh '''
                            git add .
                            git commit -m "Automated commit from Jenkins - ${BUILD_NUMBER}"
                            git remote set-url origin https://${GITHUB_TOKEN}@github.com/pulkit9897/pulkit9897.github.io.git
                            git push origin ${BRANCH_NAME}
                        '''
                    }
                }
            }
        }
    }
    
    post {
        success {
            echo 'Successfully pushed changes to GitHub!'
        }
        failure {
            echo 'Failed to push changes to GitHub'
        }
    }
}
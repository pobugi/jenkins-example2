pipeline {
    agent any

    parameters {
        gitParameter
        name: 'BRANCH',
        type: 'PT_BRANCH',
        defaultValue: 'main',
        description: 'Branch to deploy from',
        useRepository: 'https://github.com/pobugi/jenkins-example2.git'
    }

    environment {
        VENV_DIR = 'venv'
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    echo "Checking out branch: ${params.BRANCH}"
                    git branch: "${params.BRANCH}", url: 'https://github.com/pobugi/jenkins-example2.git'
                }
            }
        }

        stage('Setup Environment') {
            steps {
                script {
                    echo "Setting up the virtual environment..."
                    sh 'python3 -m venv $VENV_DIR'
                    sh '''
                    echo "Installing dependencies..."
                    $VENV_DIR/bin/pip install --upgrade pip
                    $VENV_DIR/bin/pip install -r requirements.txt
                    '''
                }
            }
        }
    }

    post {
        always {
            echo "Cleaning up workspace..."
            cleanWs()
        }
    }
}

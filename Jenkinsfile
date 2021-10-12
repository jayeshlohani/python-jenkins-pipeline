#!groovy

pipeline {
    agent {
        docker {
            image 'python:3.7'
        }
    }

    stages {
        stage('Environment preparation') {
            steps {
                echo "-=- preparing project environment -=-"
                // Python dependencies
                sh "pip install -r requirements.txt"
            }
        }
        stage('Compile') {
            steps {
                echo "-=- compiling project -=-"
                sh "python -m compileall ."
            }
        }

        stage('Unit tests') {
            steps {
                echo "-=- execute unit tests -=-"
                sh "nosetests -v test"
            }
        }
    }

    post {
        always {
            echo "-=- remove deployment -=-"
            sh "docker stop python-jenkins-pipeline"
        }
    }
}

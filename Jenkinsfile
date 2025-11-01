pipeline {
    agent any
    
    stages {
        stage('Code') {
            steps {
                echo "Cloning GitHub repo"
                git url: 'https://github.com/kaif-alam-46/node-todo-cicd.git', branch: 'master'
            }
        }

        stage('Build') {
            steps {
                sh 'docker build . -t kaifalam46/node-todo-test:latest'
            }
        }

        stage('Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerHub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh "echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin"
                    sh 'docker push kaifalam46/node-todo-test:latest'
                }
            }
        }

        stage('Test') {
            steps {
                echo "Testing the new build..."
            }
        }

        stage('Deploy') {
            steps {
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}

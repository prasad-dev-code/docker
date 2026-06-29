pipeline {

    agent any

    parameters {
        choice(
            name: 'BRANCH',
            choices: ['q1', 'q2', 'q3'],
            description: 'Select the branch to deploy'
        )
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: "${params.BRANCH}",
                    url: 'https://github.com/prasad-dev-code/docker.git'
            }
        }

        stage('Create HTTPD Container') {
            steps {
                sh '''
                docker rm -f httpd-container || true

                docker run -d \
                  --name httpd-container \
                  -p 8081:80 \
                  httpd
                '''
            }
        }

        stage('Deploy HTML') {
            steps {
                sh '''
                docker cp index.html httpd-container:/usr/local/apache2/htdocs/index.html
                '''
            }
       }
    }
}

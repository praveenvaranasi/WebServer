pipeline {
    agent any
    parameters {
        string(description: 'message to be displayed as header in the webserver', name: 'Message')
    }
    
    stages {
        stage('Build') {
            steps {
               echo 'hello'
            }
        }
    }
    post {
        always {
            echo 'Running Cleanup Step'
            cleanWs()     
        }
    }
}

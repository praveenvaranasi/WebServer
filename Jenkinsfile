pipeline {
    agent any
    parameters {
        string(description: 'message to be displayed as header in the webserver', name: 'Message')
    }
    
    stages {
        stage('Build') {
            steps {
                sh '''
                    echo "----> Building the Image"
                    echo "----> Listing the contents in the repo: `ls -l`"
                    
                    sed -i "s/message/${Message}/g" index.html
                    sed -i "s/BUILD/${BUILD_NUMBER}/g" index.html

                    echo '----> Printing out the content of index.html'
                    cat index.html
                    cat Jenkinsfile
                    docker build . -t tapan111/webserver-tapan:${BUILD_NUMBER}                                                                                     "
                '''
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

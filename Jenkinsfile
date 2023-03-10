pipeline {
    agent any
    parameters {
        string(description: 'message to be displayed as header in the webserver', name: 'Message')
    }
    
    stages {
        stage('Build') {
            steps {
               sh '''#! /bin/bash
                    echo "----> Building the Image"
                    echo "----> Listing the contents in the repo: `ls -l`"
                    
                    sed -i "s/message/${Message}/g" index.html
                    sed -i "s/BUILD/${BUILD_NUMBER}/g" index.html

                    echo '----> Printing out the content of index.html'
                    cat index.html
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

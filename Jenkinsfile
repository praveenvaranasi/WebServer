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
                    docker build . -t tapan111/webserver-tapan:${BUILD_NUMBER}
               '''
            }
        }
        stage('Push the Image') {
            steps {
                sh ''' #! /bin/bash
                    echo '----> Pushing the image to Dockerhub'
                    #docker push tapan111/webserver-tapan:${BUILD_NUMBER}    
                '''
            }
        }
        stage('Deploy') {
            steps {
                sh ''' #! /bin/bash
                    docker stop $(docker ps -aq) || true
                    docker rm $(docker ps -aq) || true
                    echo '----> Launching the container'
                    docker run -d --rm -p 8081:80 tapan111/webserver-tapan:${BUILD_NUMBER}
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

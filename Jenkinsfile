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

                    echo "----> Printing out the content of index.html" 
                    cat index.html
                    
                    docker build . -t tapan111/webserver-tapan:${BUILD_NUMBER}

                    echo '----> Printing out the images'
                    docker images                                                                                       "
                '''
            }
        }
        stage('Push the Image') {
            steps {
                sh '''#! /bin/bash
                    echo '----> Pushing the image to Dockerhub'
                    docker push tapan111/webserver-tapan:${BUILD_NUMBER}
                '''
            }
        }
        stage('Deploy') {
            steps {
                sh '''
                    echo '----> Launching the container'
                    docker run --rm -p 8080:80 tapan111/webserver-tapan:${BUILD_NUMBER} -d 
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

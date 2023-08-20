pipeline {
    agent any
           
        stage('Build') {
            steps {
                script {
                    // Create the helloworld.py file with the specified content
                    echo "building the helloworld.py file.."
                    echo "print('hello world')" > helloworld.py
                }
            }
        }
        
        stage('Test') {
            steps {
                script {
                    // Display the content of helloworld.py using the 'type' command
                    echo "Verifying the file content"
                    cat helloworld.py
                }
            }
        }
        
        stage('Deploy') {
            steps {
                script {

                    echo "Deploying code into GitHub"
                    // The credentials you've configured in Jenkins will be used here
                    // Just specify the repository URL and Jenkins will handle authentication
                    def scmVars = checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/Poterman/Jenkins.git']]])
                    
                    // Commit and push the changes back to the repository
                    sh '''
                        git add helloworld.py
                        git commit -m "Update helloworld.py"
                        git push origin main  // Assuming main is the default branch
                    '''
                }
            }
        }
    }
}

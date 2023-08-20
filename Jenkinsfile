pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout the repository
                checkout scm
            }
        }

        stage('Build') {
            steps {
                script {
                    // Create the helloworld.py file with the specified content
                    echo "building the helloworld.py file.."
                    sh 'echo "print(\'hello world\')" > helloworld.py'
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    // Display the content of helloworld.py using the 'type' command
                    echo "Verifying the file content"
                    sh 'cat helloworld.py'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    echo "Deploying code into GitHub"
                    // The credentials you've configured in Jenkins will be used here
                    // Just specify the repository URL and Jenkins will handle authentication
                    def scmVars = checkout([$class: 'GitSCM', branches: [[name: '*/master']], userRemoteConfigs: [[url: 'https://github.com/Poterman/Jenkins.git']]])

                    // Commit and push the changes back to the repository
                    sh '''
                        git config user.email "daniel.poterman@gmail.com"
                        git config user.name "Poterman"
                        git add helloworld.py
                        git commit -m "Update helloworld.py"
                        git push origin master
                    '''
                }
            }
        }
    }
}

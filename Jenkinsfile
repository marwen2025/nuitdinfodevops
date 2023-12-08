pipeline {
    agent any

    stages {

        stage('Extract and Transfer Code to GitHub') {
            steps {
                script {
                    // Supprimer le répertoire s'il existe déjà
                    sh 'sudo rm -rf extracted-code'
                    // Create a temporary directory
                    sh 'mkdir extracted-code'

                    // Run a container to extract the code from the Docker image
                    sh 'sudo docker create --name temp-container viconee/training:latest'
                    sh 'sudo docker cp temp-container:/usr/src/app extracted-code'
                    sh 'sudo docker rm temp-container'

                    // Clone the GitHub repository
                    git clone 'git@github.com:marwen2025/nuitdinfodevops.git'

                    // Copy the extracted code to the repository
                    sh 'cp -R extracted-code/* nuitdinfodevops/'

                    // Commit and push the changes to GitHub
                    dir('nuitdinfodevops') {
                        git 'config --global user.email "marwenjaballah23@gmail.com"'
                        git 'config --global user.name "viconee"'
                        git 'add .'
                        git 'commit -m "Update code from Docker image"'
                        git 'push origin main'
                    }
                }
            }
        }
    }
}

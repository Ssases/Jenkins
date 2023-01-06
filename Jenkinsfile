pipeline {
    agent any

    stages {
        stage('setgitconfig') {
             sh 'git config --global user.email "test@test.com"'
             sh 'git config --global user.name "ci-bot"'
             sh 'git config --global credential.helper cache'
             sh "git config --global credential.helper 'cache --timeout=3600'"
            }
        stage('setgitcreds') {
             git credentialsId: 'PAT_TOKEN', url: 'https://github.com/Ssases/upload.git'
             git credentialsId: 'PAT_TOKEN', url: 'https://github.com/Ssases/upload-copy.git'
            }
        stage('Syncronize TFS-SECOND'){
        sh 'git clone https://ssases:$PAT_TOKEN@github.com/Ssases/upload.git'
        dir("upload") {
            //add a remote repository
            sh 'git remote add --mirror=fetch upload-copy https://ssases:$PAT_TOKEN@github.com/Ssases/upload-copy.git'
            // update the local copy from the first repository
            sh 'git fetch origin --tags'

            // update the local copy with the second repository
            sh 'git fetch upload-copy --tags'

            // sync back the second repository
            sh 'git push upload-copy --all'
            sh 'git push upload-copy --tags'
            }
        }   
    }
}

pipeline {
    agent any
    stages {
        stage('setgitconfig') {
          steps {
             sh 'git config --global user.email "test@test.com"'
             sh 'git config --global user.name "ci-bot"'
             sh 'git config --global credential.helper cache'
             sh "git config --global credential.helper 'cache --timeout=3600'"
            }
        }
        stage('setgitcreds') {
          steps {
             git credentialsId: '7489c6b6-71b6-4a1d-98d5-4a3c27a6e8a6', url: 'https://github.com/Ssases/upload.git'
             git credentialsId: '7489c6b6-71b6-4a1d-98d5-4a3c27a6e8a6', url: 'https://github.com/Ssases/upload-copy.git'
            }
        }
        stage('Syncronize TFS-SECOND'){
          steps {
          sh 'git clone --bare upload https://github.com/Ssases/upload.git'
        dir("upload") {
            //add a remote repository
            sh 'git remote add --mirror=fetch upload-copy https://github.com/Ssases/upload-copy.git'
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
}

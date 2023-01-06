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
        
        stage('Syncronize TFS-SECOND'){
          steps {
          sh 'git clone --bare upload https://ssases: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@github.com/Ssases/upload.git'
        dir("upload") {
            //add a remote repository
            sh 'git remote add --mirror=fetch upload-copy https://ssases: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@github.com/Ssases/upload-copy.git'
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

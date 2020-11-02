//ok
pipeline {

    agent any

    environment {
        workspace = pwd()
        branch = 'master'
        url = 'https://bitbucket.org/livetouchdev/helloios'
    }

    stages {
        stage('Checkout git') {
            steps {
                git branch: branch, credentialsId: 'livetouch', url: url
            }
        }

        //https://medium.com/multinetinventiv/ci-cd-with-jenkins-docker-and-fastlane-p2-jenkins-and-docker-45960d1958fd
        stage('Build project') {
            steps {
                sh 'security -v unlock-keychain -p ricardo ~/Library/Keychains/login.keychain-db'
                sh 'source $HOME/.bash_profile'
                sh 'bundle install'
                sh 'bundle update fastlane'
                sh 'bundle exec fastlane app_center'
            }
        }
    }
}

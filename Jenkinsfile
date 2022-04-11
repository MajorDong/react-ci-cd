pipeline {
    agent {
      docker {
        image 'node:14-alpine'
        args '-p 3000:3000'
      }
    }
    environment {
        npm='npm --registry=https://registry.npm.taobao.org \
        --cache=$HOME/.npm/.cache/cnpm \
        '
    }
    stages {
        stage('Npm install') {
            steps {
                sh "${npm} --version"
                sh "${npm} install"
            }
        }
        stage('Unit test') {
            steps {
                sh "${npm} run test"
            }
        }
        stage('Npm build') {
            steps {
                sh "pwd"
                sh "${npm} run build"
                sh "tar -zcvf dist.tar ./build"
            }
        }
        stage('SSH transfer') {
            steps([$class: 'BapSshPromotionPublisherPlugin']) {
                sshPublisher(
                    continueOnError: false, failOnError: true,
                    publishers: [
                        sshPublisherDesc(
                            configName: "admin",
                            verbose: true,
                            remoteDirectory: 'jenkins/dist',
                            transfers: [
                                sshTransfer(sourceFiles: 'dist.tar'),
                                sshTransfer(execCommand: "tar xvf jenkins/dist/dist.tar -C /home/webserver/static/jenkins/dist/"),
                            ]
                        )
                    ]
                )
            }
        }
    }
}
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
        // stage('Unit test') {
        //     steps {
        //         sh "${npm} run test"
        //     }
        // }
        stage('Npm build') {
            steps {
                sh "pwd"
                sh "${npm} run build"
                sh "tar -zcvf dist.tar ./build"
            }
        }
        stage ('Deploy') {
            steps {
                sh "shh root@101.35.231.63 rm -rf /home/webserver/static/jenkins/dist"
                sh "scp dist.tar root@101.35.231.63:/home/webserver/static/jenkins/dist"
                sh "shh root@101.35.231.63 tar xvf /home/webserver/static/jenkins/dist/dist.tar"
            }
        }
    }
}
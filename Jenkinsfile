/* groovylint-disable-next-line NglParseError */
pipeline {
    agent {
      docker {
        image 'node:6-alpine'
        args '-p 3000:3000'
      }
    }
    environment {
        npm='npm --registry=https://registry.npm.taobao.org \
        --cache=$HOME/.npm/.cache/cnpm \
        '
    }
    stages {
        stage('npm build') {
            steps {
                // sh "${cnpm} i"
                // sh "${cnpm} run build"
                sh "${npm} --version"
            }
        }
        // stage ('Starting bff job') {
        //     steps{
        //     build job: 'bme-portal-bff', wait: false
        //     }
        // }
    }
}
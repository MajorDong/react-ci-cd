/* groovylint-disable-next-line NglParseError */
pipeline {
    environment {
        npm='npm --registry=https://registry.npm.taobao.org \
        --cache=$HOME/.npm/.cache/cnpm \
        '
    }
    agent {
        node {
            label 'master'
        }
    }
    stages {
        stage('npm build') {
            steps {
                // sh "${cnpm} i"
                // sh "${cnpm} run build"
                sh "npm --version"
            }
        }
        // stage ('Starting bff job') {
        //     steps{
        //     build job: 'bme-portal-bff', wait: false
        //     }
        // }
    }
}
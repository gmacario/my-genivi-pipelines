pipeline {
  agent {
    docker {
      image 'gmacario/build-yocto'
    }
    
  }
  stages {
    stage('Checkout') {
      steps {
        echo 'Checkout stage'
        git(url: 'https://github.com/GENIVI/genivi-dev-platform', branch: 'master', changelog: true)
      }
    }
    stage('Build') {
      steps {
        echo 'hello'
        sh '''#!/bin/bash -xe

# DEBUG
id
pwd
ls -la
printenv | sort

# Configure git
git config --global user.name "easy-jenkins"
git config --global user.email "$(whoami)@$(hostname)"

# Configure the build
source init.sh raspberrypi3

# Prevent error "Do not use Bitbake as root"
[ $(whoami) = "root" ] && touch conf/sanity.conf

# Perform the actual build
bitbake genivi-dev-platform
# TODO: bitbake genivi-dev-platform-sdk

# EOF'''
      }
    }
    stage('Test') {
      steps {
        parallel(
          "Chrome": {
            echo 'testing in chrome'
            
          },
          "Firefox": {
            echo 'testing in firefox'
            
          }
        )
      }
    }
    stage('Deploy') {
      steps {
        echo 'deploying'
      }
    }
  }
}

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

# Workaround for "Please use a locale setting which supports utf-8"
# See https://github.com/gmacario/my-agl-pipelines/issues/9
export LC_ALL=en_US.UTF-8
export LANG=en_US.UTF-8
export LANGUAGE=en_US.UTF-8
 
# Perform the actual build
bitbake genivi-dev-platform
# TODO: bitbake genivi-dev-platform-sdk

# DEBUG
# ls -la tmp/
# ls -la tmp/deploy/
# ls -la tmp/deploy/images
# ls -la tmp/deploy/images/raspberrypi3/

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
        echo 'INFO: Deploying'
        sh '''#!/bin/bash -xe

# DEBUG
pwd
ls -la
ls -la gdp-src-build/
ls -la gdp-src-build/tmp/
ls -la gdp-src-build/tmp/deploy/
ls -la gdp-src-build/tmp/deploy/images/
ls -la gdp-src-build/tmp/deploy/images/raspberrypi3/

# EOF'''
        archive 'gdp-src-build/tmp/deploy/images/*/*.rootfs.manifest'
        archive 'gdp-src-build/tmp/deploy/images/*/*.rootfs.rpi-sdimg'
      }
    }
  }
}

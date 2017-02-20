pipeline {
  agent {
    docker {
      image 'gmacario/build-yocto-genivi'
    }
    
  }
  stages {
    stage('Checkout') {
      steps {
        echo 'Checkout stage'
        dir('meta-ivi') {
            git(url: 'https://github.com/GENIVI/meta-ivi', branch: '12.0', changelog: true)
        }
        dir('poky') {
            git(url: 'git://git.yoctoproject.org/poky', branch: 'morty', changelog: true)
        }
        dir('meta-openembedded') {
            git(url: 'git://git.openembedded.org/meta-openembedded', branch: 'morty', changelog: true)
        }
        sh '''#!/bin/bash -xe

pwd
ls -la

cd meta-ivi
scripts/checkout_layer_hash.sh poky
scripts/checkout_layer_hash.sh meta-openembedded
cd -
# EOF'''
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

# Workaround for "Please use a locale setting which supports utf-8."
export LC_ALL=en_US.UTF-8
export LANG=en_US.UTF-8
export LANGUAGE=en_US.UTF-8 

# Configure the build
export TEMPLATECONF=${PWD}/meta-ivi/meta-ivi/conf
source poky/oe-init-build-env

# Prevent error "Do not use Bitbake as root"
[ $(whoami) = "root" ] && touch conf/sanity.conf

export MACHINE=vexpressa9

# Perform the actual build
bitbake nostromo-image
# TODO: bitbake test-image

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

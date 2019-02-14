pipeline {
  agent {
    node {
      label 'bare-metal'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh 'docker run --rm -v `pwd`:/go/src/github.com/intel/pmem-csi pmem-csi-ci:go-alpine  make'
      }
    }
    stage('Test') {
      steps {
        sh 'docker run --rm -v `pwd`:/go/src/github.com/intel/pmem-csi pmem-csi-ci:go-alpine  make test'
      }
    }
  }
  post {
      always {
         sh 'docker run --rm -v `pwd`:/go/src/github.com/intel/pmem-csi pmem-csi-ci:go-alpine make clean'
	 sh 'docker run --rm -v `pwd`:/go/src/github.com/intel/pmem-csi pmem-csi-ci:go-alpine rm -rf _work'
	 deleteDir()
      }
  }
}
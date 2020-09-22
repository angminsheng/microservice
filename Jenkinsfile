@Library('infra-jenkins-library') _
​
pipeline {
    agent {
        kubernetes {
            label 'e2e'
            defaultContainer 'jnlp'
            idleMinutes 30
            activeDeadlineSeconds 300
            yaml libraryResource('se/amboss/jenkins/pipeline/lib/slave-template.yaml')
        }
    }
    environment {
        APP_NAME = "hello_world"
        DOCKER_REGISTRY = 'eu.gcr.io/medicuja'
        RELEASE_VERSION = "${BRANCH_NAME}-${BUILD_NUMBER}"
    }
    options {
        buildDiscarder(logRotator(numToKeepStr: '200', artifactNumToKeepStr: '200'))
        skipDefaultCheckout()
    }
    stages {
        stage('Build the image') {
            steps {
                sh "docker build -t ${DOCKER_REGISTRY}/${APP_NAME}:${RELEASE_VERSION} ."
            }
        }
        stage('Test the image') {
            steps {
                sh "echo not configured"
            }
        }
        stage('Push the image') {
            steps {
                sh "docker push ${DOCKER_REGISTRY}/${APP_NAME}:${RELEASE_VERSION}"
            }
        }
    }
}

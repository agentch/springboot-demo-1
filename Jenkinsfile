#!/usr/bin/env groovy

node("master"){
    // tool name: 'mvn', type: 'maven'
    // def MVN_HOME=tool 'mvn'
    // env.PATH = "${MVN_HOME}/bin:${env.PATH}"
    stage("checkout"){
        checkout scm
        sh "ls -al"
        sh "pwd"
    }
    stage("package"){
            sh "pwd"
            sh "ls -al"
            withMaven (maven: 'mvn') {
                sh "mvn -v"
                sh "mvn package -Dmaven.test.skip=true"
            }
        }
    
    sh 'java -version'
    sh 'git --version'
    stage("hygieia"){
        hygieiaBuildPublishStep buildStatus: 'Success'
        hygieiaArtifactPublishStep artifactDirectory: 'target', artifactGroup: 'com.syna.ci', artifactName: 'springboot-demo*.jar', artifactVersion: ''
        hygieiaDeployPublishStep applicationName: 'SpringBoot', artifactDirectory: 'target', artifactGroup: 'com.syna.ci', artifactName: 'springboot-demo*.jar', artifactVersion: '', buildStatus: 'Success', environmentName: 'Dev'
    }
}

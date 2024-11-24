pipeline{
    agent any
    tools{
        maven 'Maven'
    }
    environment {
        dockerhub_cred = credentials('docker-cred')
    }
    stages{
        stage('Checkout stage'){
            steps{
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/DevopsWorking/addressbook.git']])
            }
        }
        stage('maven build'){
            steps{
                sh 'mvn package' // war package -- web app
            }
        }
        stage('docker build'){
            steps{
                sh 'docker build -t lowyiiii/addressbook:${BUILD_NUMBER} .'
            }
        }
        stage('list images'){
            steps{
                sh 'echo $dockerhub_cred_PSW | docker login -u $dockerhub_cred_USR --password-stdin'
                sh 'docker push lowyiiii/addressbook:${BUILD_NUMBER}'
            }
        }
    }
}

pipeline {
    agent any
    environment {
        APP_HOME='/home/app'
        PRAGRA_BATCH='devs'
    }
    options { 
        quietPeriod(30) 
    }
    parameters { 
            choice(name: 'ENV_TO_DEPLOY', 
            choices: ['ST', 'UAT', 'STAGING'], description: 'Select a Env to deploy') 

             booleanParam(name: 'RUN', defaultValue: true, description: 'SELECT TO RUN')
    }
//     triggers {
//         pollSCM('* * * * *')
//     }
    tools{
        maven  'm3'
        jdk 'jdk11'
    }

    stages {
        stage('Clean Ws') {
            steps{
                cleanWs()
            }
        }
        stage('Git CheckoutOut'){
            steps{
                checkout scm
            }
        }
        stage('Compile') {
            steps {
                sh 'mvn compile'
            }
        }
       stage('Static Code Analaysis') {
            steps {
                withSonarQubeEnv(credentialsId: 'sonar', installationName: 'sonarcloud') {
                    sh 'mvn sonar:sonar'
                }
            }
        }
         stage('Unit Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Docker Login') {
            steps {
                sh 'docker login -u sreejagajelli -p "Maple@2021"'
            }
        }
        stage('Docker Build Image') {
            steps {
                sh 'docker build -t sreejagajelli/test_security:latest .'
            }
        }
        stage('Docker Push Image') {
            steps {
                sh 'docker push sreejagajelli/test_security:latest'
            }
        }

         stage('Package') {
            steps {
                sh 'mvn package'
            }
        }
    }

    post {
        always {
            echo 'ALL GOOD'
            sh 'docker logout'
        }
    }


}

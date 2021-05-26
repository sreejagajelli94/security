node ('ubuntu1804') {
    def Author = 'Sreeja Gajelli'

    stage('Clean WS') {
        sh 'echo "Cleaning WorkSpace"'
        cleanWs();

    }
    stage('Declartive Checkout'){
        checkout scm;
    }
    stage('Compile') {
        withMaven(jdk: 'jdk11', maven:'m3') {
            sh 'mvn compile'
        }
    }
     stage('Test') {
        withMaven(jdk: 'jdk11', maven:'m3') {
            sh 'mvn test'

        }
    }
    
    stage('Unit Test') {
        withMaven(jdk: 'jdk11', maven:'m3') {
            sh 'mvn test'

        }
    }

     stage('Package') {
        withMaven(jdk: 'jdk11', maven:'m3') {
            sh 'mvn package'
        }
    }

    stage('Upload To Artifactory') {
        withMaven(jdk: 'jdk11', maven:'m3') {
            sh 'mvn install'
        }
    }
    stage('Who Completed') {
        sh "echo ${Author}"
    }

}

pipeline {
    agent any
    environment {
        PATH = "/opt/maven/bin:$PATH"
    }
    stages {
        stage('git clone') {
            steps {
                git url: 'https://github.com/anwar9978/IRCTC.git', branch:'main'
            }
        }
        stage('build') {
            steps {
                sh 'mvn clean deploy'
            }
        }
        stage('SQanalysis') {
            environment {
                scannerHome = tool 'SQ Scanner'
            }
            steps {
               withSonarQubeEnv('Anwar_SQ'){
                  sh "${scannerHome}/bin/sonar-scanner"
                  }
            }
        }
    }
}

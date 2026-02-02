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
                echo 'build started'
                sh 'mvn clean package -Dmaven.test.skip=true'
                echo 'build completed'
            }
        }
        stage('test') {
            steps {
                echo 'testing started'
                sh 'mvn test'
                sh 'mvn surefire-report:report'
                echo 'testing  completed'
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

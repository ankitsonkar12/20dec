pipeline {
    agent any
    tools {
        maven "m3"
        jdk "jdk8"
    }
    triggers {
            pollSCM("* * * * *")
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                sh "mvn clean compile"
            }
        }
        stage('Test') {
            steps {
                echo 'Testing'
                sh "mvn test"
            }
        }
        stage('Test Report') {
          steps {
              script {
                junit '**/surefire-reports/*.xml'
              }
          }
        }
        stage('Sonar Analysis') {
            steps {
                echo 'Sonar Scanner'
               	withSonarQubeEnv('sonarqube') {
			    	sh "mvn sonar:sonar"
			    }
            }
        }
        stage('Package') {
            steps {
                echo 'Packaging'
                sh "mvn package -DskipTests"
            }
        }
        stage('Deploy') {
            steps {
                echo '## TODO DEPLOYMENT ##'
                echo 'Add a deployment enviroment'
            }
        }
        
    post {
        always {
            echo 'JENKINS PIPELINE'
        }
        success {
            echo 'JENKINS PIPELINE SUCCESSFUL'
        }
        failure {
            echo 'JENKINS PIPELINE FAILED'
        }
        unstable {
            echo 'JENKINS PIPELINE WAS MARKED AS UNSTABLE'
        }
        changed {
            echo 'JENKINS PIPELINE STATUS HAS CHANGED SINCE LAST EXECUTION'
        }
    }
}
}

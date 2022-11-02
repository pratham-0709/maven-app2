pipeline{
    agent any
    tools {
        maven 'Maven'
    }
    stages{
        stage("TEST"){
            steps{
                sh 'ls'
                sh 'mvn -version'
                sh 'mvn test'
                echo 'Done Test'
            }
        }
        stage("BUILD"){
            steps{
                sh "mvn package"
                echo 'Done Build'
            }
        }
        stage("DEPLOY ON TEST"){
            steps{
                deploy adapters: [tomcat9(credentialsId: 'tomcat9details', path: '', url: 'http://20.121.120.44:8080')], contextPath: '/app', war: '**/*.war'
                echo "Deploying On Test Server"
            }
        }
        stage("DEPLOY ON PROD"){
            steps{
                deploy adapters: [tomcat9(credentialsId: 'tomcat9detail1', path: '', url: 'http://20.193.135.184:8080')], contextPath: '/app', war: '**/*.war'
                echo 'Hello Prod Server'
            }
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}

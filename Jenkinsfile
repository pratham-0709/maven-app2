pipeline{
    agent any
    tools {
        maven 'Maven Home'
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
                deploy adapters: [tomcat9(credentialsId: 'tomcat9details', path: '', url: 'http://20.193.151.193:8080')], contextPath: '/app', war: '**/*.war'
                echo "Deploying On Test Server"
                echo 'Done'
            }
        }
        stage("DEPLOY ON PROD"){
            input{
                message "Should We Continue?" 
                ok 'Yes We Should!'
            }
            steps{
                deploy adapters: [tomcat9(credentialsId: 'tomcat9details1', path: '', url: 'http://20.199.20.50:8080')], contextPath: '/app', war: '**/*.war'
                echo 'Done! Hello From Prod Server'
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


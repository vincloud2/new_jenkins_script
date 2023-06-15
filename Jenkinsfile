pipeline {
    agent { label "slave1" }
    
    triggers {
        pollSCM('* * * * *')    
    }
    stages {
        stage('Stage1_clone') {
            steps {
                echo 'clone my project'
                git 'https://github.com/vincloud2/Helloworld-latest.git'
            }
        }
        stage('Stage2_Build') {
            steps {
                echo 'Build my project'
                sh 'yum install maven -y'
                sh 'mvn -Dmaven.test.failure.ignore=true install'
            }
        }
        stage('Stage3_Deploy') {
            steps {
                echo 'Deploy my project'
                deploy adapters: [tomcat8(credentialsId: 'tomcat_admin', path: '', url: 'http://54.254.172.220:8080/')], contextPath: null, war: '**/*.war'
            }
        }
        stage('Stage4_Test') {
            steps {
                echo 'Test my project'
            }
        }        
    }
}

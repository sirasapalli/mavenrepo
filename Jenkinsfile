pipeline{
    agent { label 'dev'}
    triggers{pollSCM '* * * * *'}
    stages{
        stage('scm'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/feat01']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/sirasapalli/mavenrepo.git']]])
            }
        }
        stage('build'){
            steps{
                sh 'mvn package'
            }
        }
        stage('sonar'){
            steps{
                withSonarQubeEnv('sonarqube') {
                sh 'mvn sonar:sonar'
                }
               
            }
        }
        stage('nexus'){
            steps{
                sh 'mvn deploy'
            }
        }
        stage('tomcat'){
            steps{sh 'scp /root/workspace/sample/target/studentapp-2.1.1-FEAT01-SNAPSHOT.war root@172.31.22.171:/var/lib/tomcat/webapps'
                
            }
        }
    }
    
}

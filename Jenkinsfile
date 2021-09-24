pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git credentialsId: 'git-cred', url: 'https://github.com/doddaprakash/maven-web-application.git'

                // Run Maven on a Unix agent.
                //sh "mvn -Dmaven.test.failure.ignore=true clean package"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
                    script{
                        withSonarQubeEnv('Sonar'){
                            sh "mvn clean sonar:sonar"
                        }
                    }
                
            }
         stage('Sonar-Analysis') {
            steps {
                  script{
                        withSonarQubeEnv('Sonar'){
                            sh "mvn clean sonar:sonar"
                        }
                    }
                
            }
          stage('Create Package') {
            steps {
                // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
                archiveArtifacts 'target/*.war'
                        }
                    }
                
            }
         stage('Create Package') {
            steps {
                sshagent(['tomcat']) {
                        sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war prakashdodda24@35.244.63.222:/opt/tomcat/apache-tomcat-8.5.71/webapps/web-app.war"
                    }
                }
            }
    }
}

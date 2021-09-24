pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git credentialsId: 'git-cred', url: 'https://github.com/doddaprakash/maven-web-application.git'
				}
                    
            }
         stage('Sonar-Analysis') {
            steps { 
                  script{
					echo "Sonar is having issue with Sonar dependency"
                    //    withSonarQubeEnv('Sonar'){
                    //        sh "mvn clean sonar:sonar"
                    //    }
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
         stage('Deploy to Tomcat') {
            steps {
                sshagent(['tomcat']) {
                        sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war prakashdodda24@35.244.63.222:/opt/tomcat/apache-tomcat-8.5.71/webapps/web-app.war"
                    }
                }
            }
    }
}

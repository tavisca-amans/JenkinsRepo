pipeline {
    agent any

tools {
  maven 'Maven'
}

    stages {
        stage('Checkout') {
            steps {
                git branch: 'release', url: 'https://github.com/tavisca-amans/java-db-Login.git'
            }
            
        }
        stage('Build') {
            steps {
   

                // Run Maven on a Unix agent.
                sh 'mvn clean package'

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
				    deploy adapters: [tomcat8(credentialsId: 'tomcat-cred', path: '', url: 'http://172.31.44.234:8080')], contextPath: 'login', war: '**/*.war'
                    //junit '**/target/surefire-reports/TEST-*.xml'
                    //archiveArtifacts 'target/*.jar'
                }
            }
        }
    }
}
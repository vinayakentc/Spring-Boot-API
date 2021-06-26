




pipeline {
    agent any
    stages {
	stage('git clone'){
	    steps{
	        git 'https://github.com/vinayakentc/Spring-Boot-API.git'
	    }
        }
		
		stage('Build') { 
          steps{ 
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
    	  }
    	
    	  post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
		}
        stage ("build1") {		//an arbitrary stage name
            steps {
                sh 'rsync -avzP  --rsh=ssh    /var/lib/jenkins/workspace/SpringBootAPI/target/SpringBootDemoProject-0.0.1-SNAPSHOT.jar ubuntu@10.200.0.104:/home/ubuntu/Springboot/'	//this is where we specify which job to invoke.
                sh "ssh  ubuntu@10.200.0.104   docker restart spring_container"

            }


        }
    }
}


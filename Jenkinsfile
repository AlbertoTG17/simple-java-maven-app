pipeline {

    agent {
        docker {
            image 'maven:3-alpine' 
            args '-v /root/.m2:/root/.m2' 
        }
    }

    stages {

        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }

	stage('Test') { 
            steps {
                sh 'mvn test' 
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml' 
                }
            }
        }

	stage('Deliver') {
            steps {
                sh 'sh './jenkins/scripts/deliver.sh'
		sh 'mvn jar:jar install:install help:evaluate -Dexpression=project.name'
		sh 'java -jar target/mvn help:evaluate -Dexpression=project.name | grep "^[^\[]"-mvn help:evaluate -Dexpression=project.version | grep "^[^\[]".jar'
		
            }
        }

	
    }

}

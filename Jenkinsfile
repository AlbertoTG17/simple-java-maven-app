pipeline {

    agent {
        docker {
            image 'maven:3-alpine' 
            args '-v /root/.m2:/root/.m2' 
        }
    }

    stages {

	stage('Example') {
            input {
                message "Should we continue?"
                ok "Yes, we should."
                submitter "Alberto"
                parameters {
                    string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
                }
            }
            steps {
                echo "Hello, ${PERSON}, nice to meet you!!."
            }
        }

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
                sh 'sudo ./jenkins/scripts/deliver.sh'	
            }
        }


	
	
    }

}

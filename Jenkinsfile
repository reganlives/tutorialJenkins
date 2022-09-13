pipeline {
    agent any
    parameters {
        booleanParam(name: 'Refresh',
                    defaultValue: false,
                    description: 'Read Jenkinsfile and exit.')
		    }
    stages {
        stage('Clean Up') {
            steps {
                sh 'sudo docker system prune -a -f'
            }
            }
        stage('Build') {
            steps {
                sh 'sudo docker-compose build'
            }
        }
        stage('Unit Tests') {
            steps {
                sh '''
                      python3 -m pytest ./converter/tests/test_unit.py
                      python3 -m pytest ./prime/tests/test_unit.py
                   '''
            }
        }
        stage('Integration Test') {
            steps {
                sh 'python3 -m pytest ./main/tests/test_unit.py'
            }
        }
        stage('Deploying') {
            steps {
                sh '''
                    ssh -i /home/jenkins/.ssh/new_key1 -o StrictHostKeyChecking=no ubuntu@18.218.119.15
                    sudo apt install apache2 -y
                    // sudo docker-compose -f /home/ubuntu/APIPrimeAge/docker-compose.yaml down
                    // sudo docker system prune -a -f                  
                    // sudo docker-compose -f /home/ubuntu/APIPrimeAge/docker-compose.yaml build
                '''
            }
        }
    }
}

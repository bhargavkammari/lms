pipeline {
    agent any

    stages {

        stage('Sonar Analysis') {
            steps {
                echo 'Testing ..'
                sh 'cd webapp && sudo docker run  --rm -e SONAR_HOST_URL="http://20.193.240.176:9000" -e SONAR_LOGIN="sqp_32552e8a4fa35cb7050d88ce302cd587811120af"  -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms'
            }
        }
        stage('Build LMS') {
            steps {
                echo 'Building Artifacts..'
                sh 'cd webapp && npm install && npm run build'
            }
        }
        stage('Test LMS') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying.... '
            }
        }
    }
}
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
                sh 'cd webapp && npm install && npm run build '
            }
        }
        stage('Release LMS') {
            steps {
                echo 'Store Artifacts.. '
                sh 'cd webapp && zip dist-1.zip -r dist'
                sh 'cd webapp && curl -v -u admin:admin1234 --upload-file dist-1.zip http://20.193.240.176:8081/repository/lms/'
            }
        }
        stage('Deploy LMS') {
            steps {
                echo 'Deploying.... '
                sh 'sudo rm -rf /var/www/html'
                sh 'curl -u admin:admin1234 -X GET \'http://20.193.240.176:8081/repository/lms/dist-1.zip\' --output dist.zip'
                sh 'unzip dist.zip'
                sh 'sudo cp -r dist/* /var/www/html/'
            }
        }
    }
}
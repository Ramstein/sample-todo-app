pipeline {
    agent any
    environment{
      LT_BUILD_NAME = "lambdatest-pipeline"
    }
    stages {
      stage('Setup') {
        steps {
          sh 'sudo wget https://downloads.lambdatest.com/tunnel/v3/linux/64bit/LT_Linux.zip'
          sh 'sudo apt-get install zip unzip'
          sh 'sudo unzip -o LT_Linux.zip'
          sh 'sudo ./LT --user ${LT_USERNAME} --key ${LT_ACCESS_KEY} --tunnelName jenkins-tunnel -infoAPIPort 8080 &'
        }
      }

      stage('Test') {
        steps {
          // One or more steps need to be included within the steps block.
          sh 'sudo sleep 5'
          sh 'sudo python3 -m http.server 8081 &'
          sh 'sudo python3 test_sample_todo_app.py'
          sh 'sudo pkill -f http.server'
          sh 'sudo sleep 10'
          sh 'sudo curl -X DELETE http://127.0.0.1:8000/api/v1.0/stop'
        }
      }

    }
}

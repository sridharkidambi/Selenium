pipeline {
   agent any

   parameters{
      

      string(name: 'JENKINS_ACCESS_KEY_ID',
      defaultValue: 'AKIAXXFZRLIBQATYLW23',
      description: 'JENKINS_ACCESS_KEY_ID')

      password(name: 'JENKINS_SECRET_ACCESS_KEY',
      defaultValue: 'X1JZ/DjO9mh5FI2SLBIf1Dh6NaDDF+T/1V/4QYgQ',
      description: 'JENKINS_SECRET_ACCESS_KEY')

      string(name: 'DEFAULT_REGION',
      defaultValue: 'us-east-1',
      description: 'DEFAULT_REGION')

     
   }

   stages {

    stage('Checkout') {
         steps {
        git 'https://github.com/sridharkidambi/Selenium.git '

        }
       }
      stage('Run application docker image') {


         steps {
            sh 'aws configure set aws_access_key_id ${JENKINS_ACCESS_KEY_ID}'
            sh 'aws configure set aws_secret_access_key ${JENKINS_SECRET_ACCESS_KEY}'
            sh 'aws configure set default.region ${DEFAULT_REGION}'
            sh 'sudo docker stop $(docker ps -a -q)'
            sh 'sudo docker rm $(docker ps -a -q)'
            sh 'sudo `aws ecr get-login --no-include-email`'
            sh 'sudo docker pull 530817571331.dkr.ecr.us-east-1.amazonaws.com/docker-image:vinaynew'
            sh 'sudo docker run -d -i -p 8081:8081 530817571331.dkr.ecr.us-east-1.amazonaws.com/docker-image:vinaynew '
            sh 'wget https://dl.google.com/linux/direct/google-chrome-stable_current_x86_64.rpm'
            sh 'sudo yum localinstall google-chrome-stable_current_x86_64.rpm -y'
            sh 'wget https://chromedriver.storage.googleapis.com/2.41/chromedriver_linux64.zip'
            sh 'unzip chromedriver_linux64.zip'
            sh 'sudo mv chromedriver /usr/bin/chromedriver'
            sh 'sudo chown root:root /usr/bin/chromedriver'
            sh 'sudo chmod +x /usr/bin/chromedriver'


         }

      }

      stage('Run ATTD') {


         steps {

            sh 'sudo pip install virtualenv'
            sh 'sudo python -m virtualenv env'
            sh 'source env/bin/activate'
            sh 'sudo pip install -r requirements.txt'
            sh 'behave'

         }

      }

  }

}
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
            sh 'aws ecr get-login --no-include-email'
            sh 'docker pull 530817571331.dkr.ecr.us-east-1.amazonaws.com/docker-image:vinaynew'
            sh 'docker run -it -p 8081:8081 530817571331.dkr.ecr.us-east-1.amazonaws.com/docker-image:vinaynew -d'

         }

      }

      stage('Run ATTD') {


         steps {

            sh 'python -m virtualenv env'
            sh 'source env/bin/activate'
            sh 'sudo pip install -r requirements.txt'
            sh 'behave'

         }

      }

  }

}
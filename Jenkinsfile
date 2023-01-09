pipeline {
    agent any

    stages {
        stage('Git checkout') {
            steps {
                   git credentialsId: '6de27308-1c85-4146-a7a9-89e096946d44', url: 'https://github.com/Saikumar85995/ecomm.git'
            }
        }
        stage('Build') {
            steps {
                sh "/usr/share/maven/maven/bin/mvn package"
                sh "mv target/*.war target/ecom.war"

            }
        }
        stage('Deploy') {
            steps {
                sshagent(['tomcat']) {
                  sh """
                       scp -o StrictHostKeyChecking=no target/ecom.war ec2-user@172.31.11.80:/home/ec2-user/apache-tomcat-10.0.27/webapps/
                       ssh ec2-user@172.31.11.80 /home/ec2-user/apache-tomcat-10.0.27/bin/shutdown.sh
                       ssh ec2-user@172.31.11.80 /home/ec2-user/apache-tomcat-10.0.27/bin/startup.sh
                    """
                 }
            }
        }    
    }
}

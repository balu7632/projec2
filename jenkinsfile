pipeline{
    agent any
    
    environment{
        PATH = "/opt/maven/apache-maven-3.8.4/bin:$PATH"
    }
    stages{
        stage("Git Checkout"){
            steps{
                git 'https://github.com/balu7632/maven-project1.git'
            }
        }
        stage("Maven Build"){
            steps{
                sh "mvn clean package"
                sh "mv target/*.war target/myweb.war"
            }
        }
        stage("deploy-dev"){
            steps{
                sshagent(['tomcat-node-1']) {
                sh """
                    scp -o StrictHostKeyChecking=no target/myweb.war  ec2-user@65.0.184.188:/opt/apache-tomcat-10.0.16/webapps/
                    
                    ssh ec2-user@65.0.184.188 /opt/apache-tomcat-10.0.16/bin/shutdown.sh
                    
                    ssh ec2-user@65.0.184.188 /opt/apache-tomcat-10.0.16/bin/startup.sh
                
                """
            }
            
            }
        }
    }
}

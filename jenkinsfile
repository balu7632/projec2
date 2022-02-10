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
    }
}

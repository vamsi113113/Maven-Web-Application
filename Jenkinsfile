node{

def mavenHome= tool name: "maven"

properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '5', artifactNumToKeepStr: '5', daysToKeepStr: '15', numToKeepStr: '5')), pipelineTriggers([githubPush()])])

stage('Github Checkout')
{
    git branch: 'Testin12april', credentialsId: 'e5f99023-f644-4f97-bc9a-697f44aea9c0', url: 'https://github.com/vamsi113113/Maven-Web-Application.git'
}
stage('Maven Build')
{
sh "${mavenHome}/bin/mvn clean package"
}
stage('Deploy into Tomcat Server')
{
sshagent(['5f45180a-14c9-472f-a021-05e01ce3c7b1'])
{
sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@18.233.97.113:/opt/apache-tomcat-9.0.73/webapps/"
}
}
stage('SendEmailNotification')
{
emailext body: '''Build Success

Please check logs if its fails

From,
Vamsidhar Reddy,
DevOps Consultant

''', subject: 'Build Success ', to: 'devops100000@gmail.com, vamsidhar2992@gmail.com'
}
}
node{
    
def mavenHome = tool name: "maven3.8.6"
    
stage('checkout'){
git branch: 'development', credentialsId: 'ccb9a0a7-7192-4807-8e52-465ff54f1b53', url: 'https://github.com/Dillrani143/maven-web-application.git'
}
stage('Build'){
sh "${mavenHome}/bin/mvn clean package"
}

stage('ExecuteSonarQubeReport'){
sh "${mavenHome}/bin/mvn sonar:sonar"
}
stage('uploadArtifcatsIntoArtifactoryRepo'){
sh "${mavenHome}/bin/mvn clean deploy"
}

stage('deployAppIntoTomcatServer'){
sshagent(['a46b0dc1-87ad-4213-8dc5-484103e5948e']) {
sh "scp  -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@172.31.39.45:/opt/apache-tomcat-9.0.65/webapps/"
}
}

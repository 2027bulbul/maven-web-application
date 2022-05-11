node {

def mavenHome = tool name : "maven3.8.5"

//taking code from git
stage('gitchcekout'){
git branch: 'master', credentialsId: '6eb21e37-c1c7-4e74-a258-bef1dae14122', url: 'https://github.com/2027bulbul/maven-web-application.git'
}

//build code
stage ('mavenBuild'){
sh "$mavenHome/bin/mvn clean package"
}



//upload build into artifact
stage ('builDeployArtifactoryNexus'){
sh "$mavenHome/bin/mvn deploy"
}

//Deploy application to Tomcat server
stage ('DeplotToTomcatServer'){
sshagent(['171eb398-2dfa-4d21-bcaa-b43b06ee5c1e']) {
    sh "scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/Job-scriptedWay/target/maven-web-application.war ec2-user@3.110.104.220:/opt/apache-tomcat-9.0.62/webapps"
}

}

}

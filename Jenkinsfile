echo "BRANCH_NAME is :- ${env.BRANCH_NAME}"
echo "BUILD_NAME is :-  ${env.BUILD_NUMBER}"
echo "JOB_NAME is :-${env.JOB_NAME}"
echo "JENKINS_NAME is :-  ${env.JENKINS_HOME}"
echo "JENKINS_URL is :- ${env.JENKINS_URL}"
echo "JOB_NAME is :- ${env.JOB_NAME}"



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
sshagent(['9f6898d1-da73-423e-ae63-3038dc8d0b77']) {
    sh "scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/Job-scriptedWay/target/maven-web-application.war ec2-user@3.110.135.117:/opt/apache-tomcat-9.0.62/webapps"
}

}

}

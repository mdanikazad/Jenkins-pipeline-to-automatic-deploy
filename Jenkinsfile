node {
  stage('prepare'){
    git(
      url: 'anishazad@bitbucket.org/anishazad/jhipster_app.git',
      credentialsId: '37101439-1799-4333-bb94-dad4155dfbb8',
      branch: 'development'
    )
  }
   stage('Build') {
      sh './mvnw -Pprod clean package -DskipTests'
   }
   stage('Deploy') {
      steps{
         sshagent(['deploy_user']) {
      
      sh 'scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/dev-bridge_pipe/target/*.war ec2-user@ 3.93.3.126:/home/ec2-user/ROOT.war'
      
      sh ' 
          ssh  ec2-user@ 3.93.3.126 << EOF'
          'sudo -u tomcat cp /home/ec2-user/ROOT.war /opt/tomcat/webapps/ROOT.war'
          sudo systemctl stop tomcat.service
          sudo systemctl start tomcat.service
        EOF
  }
  
}



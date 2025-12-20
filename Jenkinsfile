




pipeline
{
	
   agent any
   tools
   {
      maven "maven-3.9.6"
   }
   stages
   {
           stage('git checkout')
           {
              steps
              {
                 git branch: 'dev', url: 'https://github.com/kmahesh406/maven-webapplication-project-kkfunda.git'
              }
           }
           stage('compile')
           {
              steps
              {
                 sh "mvn compile"
              }
           }
           stage('Build')
           {
             steps
             {
               sh "mvn clean package"
             }
           }
           stage('SQ REPORT')
           {
             steps
             {
                sh "mvn sonar:sonar"
             }
           }
           stage('Deploy to nexus')
           {
              steps
              {
                sh "mvn clean deploy"
              }
           }
           stage('Deploy to tomcat')
           {
              steps
              {
                 sh """

      curl -u kk:password \
--upload-file /var/lib/jenkins/workspace/jio-declarative-pl/target/maven-web-application.war \
"http://3.7.254.52:8080//manager/text/deploy?path=/maven-web-application&update=true"
          
        """
              }
           }
            stage('airtel-qa') {
             steps {
              build job: 'airtel-qa' // this is dowstream job

             }
            }

   }  //stages ending


} //pipeline ending

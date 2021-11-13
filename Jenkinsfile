pipeline
{
    agent any
    stages
    {
        stage('Continuous Download')
        {
            steps
            {
                script
                {
                    try
                    {
                        git 'https://github.com/intelliqittrainings/maven.git'
                    }
                    catch(Exception e1)
                    {
                        mail bcc: '', body: 'Jenkins is unable to download the dev code from the github', cc: '', from: '', replyTo: '', subject: 'Download Failed', to: 'git.admin@gmail.com'
                        exit(1)
                    }
                }
                
            }
        }
         stage('Continuous Build')
         {
            steps
            {
                script
                {
                    try
                    {
                        sh 'mvn package'
                    }
                    catch(Exception e2)
                    {
                        mail bcc: '', body: 'Jenkins is unable to create an artifact from the downloaded code', cc: '', from: '', replyTo: '', subject: 'Build Failed', to: 'dev.team@gmail.com'
                        exit(1)
                    }
                }
                
            }
         }
         stage('Continuous Deployment')
         {
            steps
            {
                script
                {
                    try
                    {
                         sh 'scp /home/ubuntu/.jenkins/workspace/DeclarativePipeline1/webapp/target/webapp.war ubuntu@172.31.91.151:/var/lib/tomcat9/webapps/mytestapp.war'
                    }
                    catch(Exception e3)
                    {
                        mail bcc: '', body: 'Jenkins is unable to delpoy into the tomcat on QAServers', cc: '', from: '', replyTo: '', subject: 'Deployment Failed', to: 'middleware.team@gmail.com'
                        exit(1)
                    }
                }
              
            }
         }
         stage('Continuous Testing')
         {
            steps
            {
                script
                {
                    try
                    {
                        git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh 'java -jar /home/ubuntu/.jenkins/workspace/DeclarativePipeline/testing.jar'
                    }
                    catch(Exception e4)
                    {
                        mail bcc: '', body: 'Selenium testing has failed', cc: '', from: '', replyTo: '', subject: 'Testing Failed', to: 'qa.team@gmail.com'
                        exit(1)
                    }
                }
                
            }
         }
         stage('ContinuousDelivery')
         {
             steps
             {
                 script
                 {
                     try
                     {
                         sh 'scp /home/ubuntu/.jenkins/workspace/DeclarativePipeline1/webapp/target/webapp.war ubuntu@172.31.25.184:/var/lib/tomcat9/webapps/myprodapp.war'
                     }
                     catch(Exception e5)
                     {
                         mail bcc: '', body: 'Jenkins is unable to deploy into tomcat on prodservers', cc: '', from: '', replyTo: '', subject: 'Delivery Failed', to: 'delivery.team@gmail.com'
                         
                     }
                 }
                  
             }
         }
    }
}

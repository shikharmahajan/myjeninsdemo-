pipeline {
    agent any
    stages {
        stage ('Build Servlet Project') {
            steps {

                /*For Mac & Linux machine */
               sh  'mvn clean test package'
            }

            post{
                success{
                    echo 'Now Archiving ....'

                    archiveArtifacts artifacts : '**/*.war'
                }
            }
        }
		
		stage ('Test'){steps {junit 'target/surefire-reports/*.xml'}}

        stage ('JUNIT')
		{steps{
		realtimeJUnit('target/surefire-reports/*.xml') {
    // some block
}}
		}
      
	  
	  stage ('Deploy Build in Staging Area'){
            steps{

                build job : 'Package'

            }
        }

        stage ('Deploy to Production'){
            steps{
                timeout (time: 5, unit:'DAYS'){
                    input message: 'Approve PRODUCTION Deployment?'
                }
                
                build job : 'Package'
            }

            post{
                success{
                    echo 'Deployment on PRODUCTION is Successful'
			mail bcc: '', body: 'Hey', cc: '', from: '', replyTo: '', subject: 'Pipeline ${BUILD_NUMBER}', to: 'shikhar.mahajan@rivigo.com'
                }

                failure{
                    echo 'Deployement Failure on PRODUCTION'
                }
				
				
            }
        }
    }
}

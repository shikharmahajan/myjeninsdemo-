pipeline {
    agent any
    stages {
        stage ('Build Servlet Project') {
            steps {

                /*For Mac & Linux machine */
               sh  'mvn clean package'
            }

            post{
                success{
                    echo 'Now Archiving ....'

                    archiveArtifacts artifacts : '**/*.war'
                }
            }
        }
		
		stage ('PMD Result) {
		Steps {pmd canComputeNew: false, defaultEncoding: '', healthy: '', pattern: 'target/pmd.xml', unHealthy: ''}
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
			mail bcc: '', body: 'Hey', cc: '', from: '', replyTo: '', subject: 'Pipeline {$BUILD_NUMBER}', to: 'shikhar.mahajan@rivigo.com'
                }

                failure{
                    echo 'Deployement Failure on PRODUCTION'
                }
				
				
            }
        }
    }
}

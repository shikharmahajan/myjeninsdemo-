
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

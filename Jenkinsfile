@Library('sharedLib') _
pipeline {
    agent any
	
	environment {
	    AWS_REGION = 'us-east-1'
            bucketName = "testbucket-anne"
			stackFileName = "wp.yaml"
			VpcId = "vpc-053b338aed86f79f5"
			PubSub1 = "subnet-060175f4908d5c3ee"
			PubSub2 = "subnet-07ef4041f59516e23"
    }
	
	parameters { 
		string(
			name: 'ENV', 
			defaultValue: 'DEV', 
			description: 'Please insert the environment'
			)
		string(
			name: 'stackName', 
			defaultValue: 'myStack-anne', 
			description: 'Please insert the stack name'
			)
	}
	
    stages {
     
		stage("Push template to S3") {
			steps {
				uploadFilesToS3(stackFileName: "${stackFileName}", workingDir: "${env.WORKSPACE}/stackTemplates", bucketName: "${bucketName}")
			}
		}
		stage('Deploy Stack') {                  
                steps {
                    deploy_stack(stackName: "${stackName}", bucketName: "${bucketName}", stackFileName: "${stackFileName}", env: "${ENV}", VpcId: "${VpcId}", PublicSubnet1: "${PubSub1}", PublicSubnet2: "${PubSub2}")
                }
            }
		
		  
    }
   }

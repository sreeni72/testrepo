pipeline {
    agent any
    
    environment {
	    //TARGET_ENV = "${params.mule_env}"
	    BRANCH_NAME = "${GIT_BRANCH.split("/")[1]}"
	    BUILD_NUMBER = currentBuild.getNumber()
        NEXUS_VERSION = "nexus3"
        NEXUS_PROTOCOL = "http"
        NEXUS_URL = "localhost:8081"
        NEXUS_REPOSITORY = "maven-snapshots"
        NEXUS_CREDENTIAL_ID = "nexus.credentials"
        
    }
    stages {
		
	    stage("Checkout"){
		    steps{
			    checkout scm
			    sh "rm -rf Readme.Md .gitignore .gitattributes .git"
		    }	    
	    }
	    
	    stage("Initialise Variables") {
			steps {
			   script{
					if(env.BRANCH_NAME == "develop") {
						TARGET_ENV = "dev"
						target_rtf = "dev_entapi"
						target_host = "dev-eapi-mulesoft.nonprod.nb01.local"
					}
					if(env.BRANCH_NAME == "test") {
						TARGET_ENV = "test"
						target_rtf = "test_entapi"
						target_host = "test-eapi-mulesoft.nonprod.nb01.local"
					}
					if(env.BRANCH_NAME == "stage") {
						TARGET_ENV = "stage"
						target_rtf = "stage_entapi"
						target_host = "stage-eapi-mulesoft.nonprod.nb01.local"
					}	
                   		
                    echo "All Variables....${target_rtf}, ${target_host}, ${TARGET_ENV}...."	+ env.BRANCH_NAME				
				}
				//echo "Checkout the Code Repository..."
				//git  branch: "${brance_name}", credentialsId: "git.credentials", url: "https://github.com/sreeni72/testrepo.git"
			}
		}
	}
}

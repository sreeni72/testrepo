pipeline {
    agent any
    
    environment {
	    TARGET_ENV = "${params.mule_env}"
	    BUILD_NUMBER = currentBuild.getNumber()
        NEXUS_VERSION = "nexus3"
        NEXUS_PROTOCOL = "http"
        NEXUS_URL = "localhost:8081"
        NEXUS_REPOSITORY = "maven-snapshots"
        NEXUS_CREDENTIAL_ID = "nexus.credentials"
        //DOCKER_REPOSITORY = "sreeni72/${pom.artifactId}-${pom.version}" 
        //DOCKER_CREDENTIALS = "dockerhub_credentials"
    }
    stages {
		stage("CheckOut") {
			steps {
			    script{
					if(env.TARGET_ENV == "dev") {
						brance_name = "develop"
						target_rtf = "dev_entapi"
						target_host = "dev-eapi-mulesoft.nonprod.nb01.local"
					}
					if(env.TARGET_ENV == "test") {
						brance_name = "test"
						target_rtf = "test_entapi"
						target_host = "test-eapi-mulesoft.nonprod.nb01.local"
					}
					if(env.TARGET_ENV == "stage") {
						brance_name = "stage"
						target_rtf = "stage_entapi"
						target_host = "stage-eapi-mulesoft.nonprod.nb01.local"
					}	
                    echo "All Variables....${brance_name}, ${target_rtf}, ${target_host}...." + env.TARGET_ENV					
				}
				echo "Checkout the Code Repository..."
				git  branch: "${brance_name}", credentialsId: "git.credentials", url: "https://github.com/sreeni72/testrepo.git"
			}
		}
	}
}

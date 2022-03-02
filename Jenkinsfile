pipeline {
    agent any
    
	parameters{
	    string CURRENT_BUILD_RESULT = "SUCCESS"
	}
	
    environment {
	
		mule_cred = credentials(' ')
		nexus_cred = credentials(' ')
		brance_name = "${GIT_BRANCH.split("/")[1]}"
		group_id = readMavenPom().getGroupId()
		artifact_id = readMavenPom().getArtifactId()
		version = readMavenPom().getVersion()
		art_name = readMavenPom().getName()
			   	    
	    BUILD_NUMBER = currentBuild.getNumber()
        NEXUS_VERSION = "nexus3"
        NEXUS_PROTOCOL = "http"
        NEXUS_URL = "localhost:8081"
        NEXUS_REPOSITORY = "maven-snapshots"
        NEXUS_CREDENTIAL_ID = "nexus.credentials"
        
    }
    stages {
		stage("Set Variables") {
			steps {
			    script{
					echo "Set Variables for ${brance_name}......"
					if(env.branch_name == "develop") {
						target_env = "dev"
						target_rtf = "dev_entapi"
						replicas = "1"
						enforceDeployingReplicasAcrossNodes = "false"
						updateStrategy = "recreate"
						clustered = "false"
						target_host = "dev-eapi-mulesoft.nonprod.nb01.local"
					}
					if(env.branch_name == "test") {
						target_env = "test"
						target_rtf = "test_entapi"
						replicas = "2"
						enforceDeployingReplicasAcrossNodes = "true"
						updateStrategy = "rollingupdate"
						clustered = "true"
						target_host = "test-eapi-mulesoft.nonprod.nb01.local"
					}
					if(env.branch_name == "stage") {
						target_env = "stage"
						target_rtf = "stage_entapi"
						replicas = "2"
						enforceDeployingReplicasAcrossNodes = "true"
						updateStrategy = "rollingupdate"
						clustered = "true"
						target_host = "stage-eapi-mulesoft.nonprod.nb01.local"
					}	
                    echo "All Variables....${brance_name}, ${target_env}, ${target_rtf}, ${target_host}...." 
					echo "Set Variables for Nexus Repository...."
					if (readMavenPom().getPackaging() == "mule-application"){
						art_type = "jar"
					} else if (readMavenPom().getPackaging() == "jar") {
						art_type = "jar"
					} else {
						art_type = readMavenPom().getPackaging()
					}
					if (version.toUpperCase().contains("SANPSHOT")){
						nexus_repo = "snapshots"
					} else {
						nexus_repo = "releases"
					}
					nexus_artifact = "${art_name}-${version}-"+ readMavenPom().getPackaging() + ".${art_type}"
					echo "Nexus Artifact : ${nexus_artifact}	
				}
				//echo "Checkout the Code Repository..."
				//git  branch: "${brance_name}", credentialsId: "git.credentials", url: "https://github.com/sreeni72/testrepo.git"
			}
		}
	}
}

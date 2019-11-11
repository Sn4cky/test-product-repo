pipeline {
    agent any
	
	environment {
		PROD_CHANGED = "false"
	}
	
    stages {
		stage("change-detection") {
			when {
				anyOf {
					changeset "**/Jenkinsfile"
                    changeset "src/main/**"
				}
			}
			steps {
				script {
					sh "echo ${PROD_CHANGED}"
					PROD_CHANGED = "true"
					sh "echo ${PROD_CHANGED}"
				}
			}
		}
		stage("typescript-build") {
			when {
				expression { PROD_CHANGED == "true" }
			}
			steps {
				sh (
					script: "echo typescript-building",
					returnStdout: true
				)
			}
		}
		stage("testing") {
			when {
				expression { PROD_CHANGED == "true" }
			}
			steps {
				sh (
					script: "echo testing",
					returnStdout: true
				)
			}
		}
		stage("artifactory-publish") {
			when {
				expression { PROD_CHANGED == "true" }
			}
			steps {
				sh (
					script: "echo artifactory-publishing",
					returnStdout: true
				)
			}
		}
    }
}

pipeline {
    agent any
	
	environment {
		PROD_CHANGED = 'false'
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
					env.PROD_CHANGED = 'true'
				}
			}
		}
		stage("typescript-build") {
			when {
				expression { env.PROD_CHANGED == 'true' }
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
				expression { env.PROD_CHANGED == 'true' }
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
				expression { env.PROD_CHANGED == 'true' }
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

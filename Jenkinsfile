pipeline {
    agent any

    environment {
        // Replace "my-label" with the name of the label you want to trigger the pipeline on
        MY_LABEL = "bug1"
    }

    stages {
        stage('Fetch issue and label information') {
            steps {
                script {
                    def issueNumber = env.CHANGE_ID
                    def labelName = env.CHANGE_TARGET
                    echo "Issue number: ${issueNumber}"
                    echo "Label name: ${labelName}"
                }
            }
            when {
                expression { false }
            }
        }
        stage('Run build steps') {
            steps {
                script {
                    if (env.CHANGE_ID || env.CHANGE_TARGET) {
                        if (env.CHANGE_TARGET?.toLowerCase() == env.MY_LABEL?.toLowerCase()) {
                            // Insert build steps here
                        } else {
                            echo "Skipping build because the label '${env.MY_LABEL}' was not applied to the issue...."
                            currentBuild.result = "SUCCESS"
                        }
                    } else {
                        echo "Skipping build because no issue or label was detected..."
                        currentBuild.result = "SUCCESS"
                    }
                }
            }
        }
    }
}

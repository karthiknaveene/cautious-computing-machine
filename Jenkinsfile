pipeline {
    agent any

    stages {
        stage('Build') {
            stages {
                stage('Compile') {
                    steps {
                        echo 'Compiling...'
                        sleep 10
                    }
                }
                stage('Package') {
                    steps {
                        echo 'Packaging...'
                        sleep 5
                    }
                }
            }
        }

        stage('Registering build artifact') {
            steps {
                echo 'Registering the metadata'
                echo 'Another echo to make the pipeline a bit more complex'
                registerBuildArtifactMetadata(
                    name: "test-artifact",
                    version: "1.0.0",
                    type: "docker",
                    url: "http://localhost:1111",
                    digest: "6f637064707039346163663237383938",
                    label: "prod"
                )
                sleep 5
            }
        }

        stage('Test') {
            steps {
                echo 'Running Unit Tests...'
                sleep 5
                // Mark this stage as UNSTABLE and stop further stages
                catchError(buildResult: 'UNSTABLE', stageResult: 'UNSTABLE') {
                    error('Tests failed. Marking build as UNSTABLE and stopping pipeline.')
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying...'
                sleep 5
            }
        }
    }
}

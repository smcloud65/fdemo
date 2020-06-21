// Declarative pipelines must be enclosed with a "pipeline" directive.
pipeline {
    // This line is required for declarative pipelines. Just keep it here.
    agent any

    // This section contains environment variables which are available for use in the
    // pipeline's stages.
    environment {
	    region = "us-east-1"
        docker_repo_uri = "210068040237.dkr.ecr.us-east-1.amazonaws.com/smdemo"
		task_def_arn = "arn:aws:ecs:us-east-1:210068040237:task-definition/first-run-task-definition:2"
        cluster = "demo0"
        exec_role_arn = "arn:aws:iam::210068040237:role/ecsTaskExecutionRole"
    }
    
    // Here you can define one or more stages for your pipeline.
    // Each stage can execute one or more steps.
    stages {
        // This is a stage.
        stage('Build') {
            steps {
        // Get SHA1 of current commit
            script {
            commit_id = sh(script: "git rev-parse --short HEAD", returnStdout: true).trim()
        }
        // Build the Docker image
        sh "docker build -t ${docker_repo_uri}:${commit_id} ."
        // Get Docker login credentials for ECR
        sh "aws ecr get-login --no-include-email --region ${region} | sh"
        // Push Docker image
        sh "docker push ${docker_repo_uri}:${commit_id}"
        // Clean up
        sh "docker rmi -f ${docker_repo_uri}:${commit_id}"
                // This is a step of type "echo". It doesn't do much, only prints some text.
                //echo 'This is a sample stage'
                // For a list of all the supported steps, take a look at
                // https://jenkins.io/doc/pipeline/steps/ .
            }
        }
	// Declarative pipelines must be enclosed with a "pipeline" directive.
pipeline {
    // This line is required for declarative pipelines. Just keep it here.
    agent any

    // This section contains environment variables which are available for use in the
    // pipeline's stages.
    environment {
	    region = "us-east-1"
        docker_repo_uri = "210068040237.dkr.ecr.us-east-1.amazonaws.com/smdemo"
		task_def_arn = "arn:aws:ecs:us-east-1:210068040237:task-definition/first-run-task-definition:2"
        cluster = "demo0"
        exec_role_arn = "arn:aws:iam::210068040237:role/ecsTaskExecutionRole"
    }
    
    // Here you can define one or more stages for your pipeline.
    // Each stage can execute one or more steps.
    stages {
        // This is a stage.
        stage('Build') {
            steps {
        // Get SHA1 of current commit
            script {
            commit_id = sh(script: "git rev-parse --short HEAD", returnStdout: true).trim()
        }
        // Build the Docker image
        sh "docker build -t ${docker_repo_uri}:${commit_id} ."
        // Get Docker login credentials for ECR
        sh "aws ecr get-login --no-include-email --region ${region} | sh"
        // Push Docker image
        sh "docker push ${docker_repo_uri}:${commit_id}"
        // Clean up
        sh "docker rmi -f ${docker_repo_uri}:${commit_id}"
                // This is a step of type "echo". It doesn't do much, only prints some text.
                //echo 'This is a sample stage'
                // For a list of all the supported steps, take a look at
                // https://jenkins.io/doc/pipeline/steps/ .
            }
        }
             steps ('prismaCloudScanImage') { 
        prismaCloudScanImage ca: '', cert: '', dockerAddress: 'unix:///var/run/docker.sock', image: '${docker_repo_uri}:${commit_id}', key: '', logLevel: 'info', podmanPath: '', project: '', resultsFile: 'prisma-cloud-scan-results.json'
	     }
	     steps ('prismaCloudPublish') {prismaCloudPublish resultsFilePattern: 'prisma-cloud-scan-results.json'}
    }
}    
    }
}

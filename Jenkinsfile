//Scripted
// node {
	
// 		echo "Build"
// 		echo "Test"
// 		echo "Integration Test"

// }

//NODE 
// node {
// 	stage('Build') {
// 		echo "Build"
// 	}
// 	stage('Test') {
// 		echo "Test"
// 	}
//     stage('Integration Test') {
// 		echo "Integration Test"
// 	}

// }

//Declarative
pipeline{
	agent any
	// agent {
	// 	docker{
	// 		image 'maven:3.6.3'
	// 	}
	// }
    environment{
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:mavenHome/bin:$PATH"
	}
	stages{
		stage('Build') {
			steps{
				sh 'mvn --version'
				sh 'docker version'
                echo "Build"
				echo "PATH -> $PATH"
				echo "BUILD_NUMBER -> $env.BUILD_NUMBER"
				echo "BUILD_ID -> $env.BUILD_ID"
				echo "JOB_NAME -> $env.JOB_NAME"
				echo "BUILD_TAG -> $env.BUILD_TAG"
				echo "BUILD_URL -> $env.BUILD_URL"
				echo "GIT_BRANCH -> $env.GIT_BRANCH"
				
			}
			
		}
		stage('Test') {
			steps{
				echo "Test"
			}
		}
		stage('Integration Test') {
			steps{
				echo "Integration Test"
			}
		}
	} 
	post{
		always{
			echo "I'm awsome, running always"
		}
		success{
			echo "running just when build is successfully"
		}
        failure{
			echo "running just when build is failured"
		}
	}
}

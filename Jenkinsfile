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
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages{
		stage('Checkout') {
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
		stage('Compile') {
			steps{
				echo "Compile"
				sh 'mvn clean compile'
			}
		}
		stage('Test') {
			steps{
				echo "Test"
				sh 'mvn test'
			}
		}
		stage('Integration Test') {
			steps{
				echo "Integration Test"
				sh 'mvn failsafe:integration-test failsafe:verify'
			}
		}
		stage('Package') {
			steps{
				echo "Package"
				sh 'mvn package -DskipTests'
			}
		}
		stage('Build Docker Image') {
			steps{
				echo "Build Docker Image"
				//"docker build -t breymer/currency-exchange-devops:$env.BUILD_TAG"
				script{
                  def  dockerImage = docker.build(" breymer/currency-exchange-devops:${env.BUILD_TAG}")
				}
			
			}
		}
		stage('Push Docker Image') {
			steps{
				echo "Push Docker Image"
				docker.withRegistry("https://hub.docker.com",'dockerhub'){
					dockerImage.push();
			    	dockerImage.push('latest');
				}
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

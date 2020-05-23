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
	stages{
		stage('Build') {
			steps{
                echo "Build"
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

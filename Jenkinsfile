pipeline{
	agent{
		label{
			label "built-in"
			customWorkspace "/mnt/volume-master"
		}
	}
		stages{
			stage("clean"){
				steps{
					echo "clean"
					}
			}
			stage("build"){
				steps{
					echo "build"
					}
			}
			stage("deploy"){
				steps{
					echo "deploy"
					}
			}
			
		}
		 post { 
        always { 
            echo 'success-master'
        }
    }
}

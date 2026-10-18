pipeline {
	agent{
		label{
			label "built-in"
			customWorkspace "/mnt/volume-master"
		}
	}
	stages{
		stage("clean") {
			steps {
				echo "clean"
				sh '''
				container=$(sudo docker ps -aq --filter volume=myvol)
				if [ -n "${container}" ]
				then
				sudo docker stop ${container} && sudo docker rm ${container}
				
				sudo docker volume rm myvol
				'''
			}
		}
		stage("build") {
			steps {
				echo "build"
				sh "sudo docker volume create myvol"
				sh "sudo cp /mnt/volume-master/index.html /var/lib/docker/volumes/myvol/_data/"
				sh "sudo docker run -dp 70:80 -v myvol:/usr/local/apache2/htdocs --name a1 httpd"
				sh "sudo docker exec a1 chmod -R 777 /usr"
				
			}
		}
		stage("deploy") {
			steps {
				echo "deploy"
			}
		}

	}
	
}

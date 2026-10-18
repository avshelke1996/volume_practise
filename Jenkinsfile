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
				container=$(sudo docker ps -q)
				if [ -n "${container}" ]
				then
				sudo docker kill ${container} && sudo docker rm ${container}
				fi
				
				sudo docker volume rm myvol
				'''
			}
		}
		stage("build") {
			steps {
				echo "build"
				sh "sudo docker volume create myvol"
				sh "sudo cp /mnt/volume-master/index.html /var/lib/docker/volumes/muvolume/_data/"
				sh "sudo docker run -itdp 70:80 -v myvol:/usr/local/apache2/htdocs --name a1 httpd"
				sh "sudo docker exec -it a1 bash"
				sh "sudo chmod -R 777 /usr"
				
			}
		}
		stage("deploy") {
			steps {
				echo "deploy"
			}
		}

	}
	
}

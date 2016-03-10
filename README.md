# vagrant-ansible-docker

- https://www.jfrog.com/confluence/display/RTF/Running+with+Docker


	docker run -Pitd --name arti5 -p 8081:8081 \
	-v /home/vagrant/share/artifactory/data:/var/opt/jfrog/artifactory/data \
	-v /home/vagrant/share/artifactory/tomcat/logs:/opt/jfrog/artifactory/tomcat/logs \
	jfrog-docker-reg2.bintray.io/jfrog/artifactory-oss:latest

	export ARTIFACTORY_HOME=/home/vagrant/share/artifactory


	/opt/jfrog/artifactory/tomcat/logs/
pipeline {
		agent {
		node {
		label ('built-in')
		
		}
		}
		
		tools {
			maven "maven-home"
		}
		
		stages {
		stage ('copy-GOL') {
		steps {
		dir ('/mnt/GOL') {
		sh " rm -rf /root/.m2 "
		sh "rm -rf *"
		sh " git clone https://github.com/ronitunale/game-of-life.git"
		sh " chmod -R 777 /mnt/GOL/game-of-life"
		}
		}
		}
		
		stage ('mvn-install') {
		steps {
		dir ('/mnt/GOL/game-of-life/') {
		sh "mvn clean install"
		sh "chmod -R 777 /mnt/GOL/game-of-life "
		
		}
		}
		}
		
		stage ('copy-war') {
		steps {
		dir ('/mnt/GOL/game-of-life/') {
		sh "cp gameoflife.war /mnt/server/apache-tomcat-9.0.67/webapps"
		
		}
		}		
		}


	}

}

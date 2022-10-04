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
		sh " rm -rf /mnt/server/apache-tomcat-9.0.67/webapps/gameoflife.war"
		sh "cp /mnt/GOL/game-of-life/gameoflife-web/target/gameoflife.war /mnt/server/apache-tomcat-9.0.67/webapps"
		
		}
		}		
		}
		
		stage ('deployment-on-slave') {
		agent {
		node {
			label ('172.31.11.161')
		
			}
		
		}
		tools {
			maven "maven-home"
		}
		
		stages {
		stage ('copy-GOL') {
		steps {
		dir ('/mnt/GOL') {
		sh " sudo rm -rf /root/.m2 "
		sh "sudo rm -rf *"
		sh "sudo git clone https://github.com/ronitunale/game-of-life.git"
		sh "sudo chmod -R 777 /mnt/GOL/game-of-life"
		}
		}
		}
		
		stage ('mvn-install') {
		steps {
		dir ('/mnt/GOL/game-of-life/') {
		sh "mvn clean install"
		sh "sudo chmod -R 777 /mnt/GOL/game-of-life "
		
		}
		}
		}
		
		stage ('copy-war') {
		steps {
		dir ('/mnt/GOL/game-of-life/') {
		sh "sudo rm -rf /mnt/server/apache-tomcat-9.0.67/webapps/gameoflife.war"
		sh "sudo cp /mnt/GOL/game-of-life/gameoflife-web/target/gameoflife.war /mnt/server/apache-tomcat-9.0.67/webapps"
		
		}
		}		
		}
		
		stage ('tomcat-start-slave') {
		steps {
		dir ('/mnt/server/apache-tomcat-9.0.67/bin') {
		
		sh "sudo ./startup.sh"
		
		}
		}				
		}
		
		
		}


	}

}
}

// this is scripted way pipeline 

node {

	def mavenHome=tool name: "maven3.9.10"
	
	stage ('CheckOut'){

	git 'https://github.com/jjio-project/Maven-Web-Application-Project.git'

	}

	stage ('Build'){

	  sh "${mavenHome}/bin/mvn clean package"
	}
	/*

	stage ('SOnarQube'){

	  sh "${mavenHome}/bin/mvn sonar:sonar"

	}

	stage ('Nexus'){

	  sh "${mavenHome}/bin/mvn deploy"

	}

	*/
	stage('Deploy WAR file to Remote Server using SCP') {

	sshagent(['902f538e-2d4a-4bf4-b761-a98601d4c348']) {
    // some block
}
        // Using SCP instead of curl
        sh """
        scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/jio-pipeline/target/maven-web-application.war \
        ec2-user@3.110.104.23:/opt/apache-tomcat-9.0.115/webapps/maven-web-application.war
        """

	}


} // node end


/* 

Follow below steps to create a ssh agent key.

1. Go to Jenkins Dashboard → Manage Jenkins → Credentials

2. Click (global) → Add Credentials

3. Select:

Kind: SSH Username with private key

Username: ec2-user

Private Key: paste your .pem file content

ID: ec2-key ← (use this in pipeline)

*/

// Make sure install "sshagent" plugin

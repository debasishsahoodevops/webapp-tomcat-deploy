pipeline{
 tools{
        jdk 'JAVA_HOME'
        maven 'M2_HOME'
    }
     agent any
	  
	  stages{
	  
	  stage("checkout"){
	   steps{
	   git 'https://github.com/debasishsahoodevops/webapp-tomcat-deploy.git'
	   }
	                  }
	
	   stage("compile"){
	    steps{
		 sh 'mvn compile'
		}
		}
       stage("unit test"){
	    steps{
		 sh 'mvn test'
		}
		}
       stage("package"){
	    steps{
		 sh 'mvn clean package'
		   sh 'mv target/*.war target/myweb.war'
                
		}
	}
	stage("package"){
	    steps{
	sshagent(['tomcat']) {
    // some block
	
	sh """
                 
            scp -o StrictHostKeyChecking=no target/myweb.war ec2-user@15.206.93.206:/home/ec2-user/tomcat10/webapps/

              ssh ec2-user@15.206.93.206 /home/ec2-user/tomcat10/bin/shutdown.sh
              ssh ec2-user@15.206.93.206 /home/ec2-user/tomcat10/bin/startup.sh
            
          
          """
}	  
     
    } 
}
}
}

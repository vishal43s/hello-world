pipeline {

    agent any

    tools {
        maven 'maven-3.8.4'
    }

    stages{
     stage('Pull source code from Git'){
         steps{
             git credentialsId: 'MyGitHUb', url: 'https://github.com/vishal43s/hello-world.git'
         }

     }
     stage('build'){
         steps{
           sh 'mvn clean install -f webapp/pom.xml'
         }

     }

     stage('Upload WAR file to ansible server'){
         steps{
           sshPublisher(publishers: [sshPublisherDesc(configName: 'ansiblehost', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'ansible-playbook /opt/docker/regapp.yaml', execTimeout: 1200000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '//opt//docker', remoteDirectorySDF: false, removePrefix: 'webapp/target/', sourceFiles: 'webapp/target/*.war')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
           kubectl get pods | grep valaxy > pod.txt
         }
     }
	 
     stage('Get pods and wite to file'){
	 steps{
             sshagent(['dockerpassword']) {
    // some block
	sh 'ssh -o ssh -o StrictHostKeyChecking=no dockeradmin@10.164.250.28 kubectl get pods | grep valaxy > 123.txt'
           }
		 }
     }
	
	}


}

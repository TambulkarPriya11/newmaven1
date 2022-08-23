node('built-in') {
    stage('ContinuousDownload') {
       git 'https://github.com/intelliqittrainings/maven.git'
    }
    
    //ContinuousBuild
    stage('ContinuousBuild') {
       sh 'mvn package'
    }
    
    //ContinuousDeployment
    stage('ContinuousDeployment') {
       sh 'scp /var/lib/jenkins/workspace/ScriptedPipeline1/webapp/target/webapp.war ubuntu@172.31.8.57:/var/lib/tomcat9/webaaps/testaap.war'
    }
    
    //ContinuousTesting
    stage('ContinuousTesting') {
       git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
       sh 'java -jar /var/lib/jenkins/workspace/ScriptedPipeline1/testing.jar'
    }
    
    //ContinuousDelivery
    stage('ContinuousDelivery') {
       input message: 'Need approval from the DM! ', submitter: 'Asha'
       deploy adapters: [tomcat9(credentialsId: '631acbc5-c6ac-4221-9531-e9221e017bcc', path: '', url: 'http://172.31.5.247:8080')], contextPath: 'myprodaap', war: '**/*.war'
       
    }
}

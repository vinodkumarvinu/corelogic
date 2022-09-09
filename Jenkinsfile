pipeline{
    agent {label 'dev'}
    tools{ maven 'maven-3.8.6'}
    stages{
        stage('gitcheckout')
        {
            steps
            {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: '636b5bcf-19e9-41c1-a4f5-65c72952db44', url: 'https://github.com/vinodkumarvinu/corelogic.git']]])
            }
        }
        stage('message')
        {
            steps
            {
             echo 'welcome to devops'   
            }
        }
        stage('maven build')
        {
            steps
            {
                sh 'mvn package -f pom.xml'
            }
        }
        stage('tomcat deploy')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '4a7a9d38-5816-4c88-8a15-7a9f229279c4', path: '', url: 'http://34.125.179.115:8080/')], contextPath: 'corelogic', war: 'target/master-corelogic.war'
            }
        }
        stage('nexus upload')
        {
            steps
            {
                nexusArtifactUploader artifacts: [[artifactId: 'corelogic', classifier: '', file: 'target/master-corelogic.war', type: 'war']], credentialsId: '95ed1302-d52c-4afb-a073-d4b39ea61fc1', groupId: 'com.adaequare', nexusUrl: '34.125.101.113:8081/', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-snapshots', version: '1.0-SNAPSHOT'
            }
        }
    }
}

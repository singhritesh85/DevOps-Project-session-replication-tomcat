pipeline{
    agent{
        node{
            label "Slave-1"
            customWorkspace "/home/jenkins/2tierapp/"
        }
    }
    environment {
        JAVA_HOME="/usr/lib/jvm/java-17-amazon-corretto.x86_64"
        PATH="$PATH:$JAVA_HOME/bin:/usr/local/bin:/opt/apache-maven/bin"
    }
    parameters { 
        string(name: 'COMMIT_ID', defaultValue: '', description: 'Provide the Commit ID')
    }
    stages{
        stage("Clone-code"){
            steps{
                cleanWs()
                checkout scmGit(branches: [[name: '${COMMIT_ID}']], extensions: [], userRemoteConfigs: [[credentialsId: 'github-cred', url: 'https://github.com/singhritesh85/tomcat-session-replication.git']])
            }
        }
        stage("SonarQubeAnalysis-and-Build"){
            steps {
                withSonarQubeEnv('SonarQube-Server') {
                    sh 'mvn clean package sonar:sonar'
                }
            }
        }
        stage("Quality Gate") {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
        stage("Nexus-Artifact Upload"){
            steps{
                script{
                    def mavenPom = readMavenPom file: 'pom.xml'
                    def nexusRepoName = mavenPom.version.endsWith("SNAPSHOT") ? "maven-snapshot" : "maven-release"
                    nexusArtifactUploader artifacts: [[artifactId: 'LoginWebApp', classifier: '', file: 'target/LoginWebApp.war', type: 'war']], credentialsId: 'nexus', groupId: 'com.javawebtutor', nexusUrl: 'nexus.singhritesh85.com', nexusVersion: 'nexus3', protocol: 'https', repository: "${nexusRepoName}", version: "${mavenPom.version}"
                }    
            }
        }
        stage("Deployment"){
            steps{
                 sh 'scp -rv target/LoginWebApp.war tomcat-admin@172.31.29.80:/opt/apache-tomcat/webapps/'
                 sh 'scp -rv target/LoginWebApp.war tomcat-admin@172.31.21.131:/opt/apache-tomcat/webapps/'
            }
        }
    }
}

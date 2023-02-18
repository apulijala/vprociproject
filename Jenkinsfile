pipeline{
    agent any 
    tools {
        maven "MAVEN3"
        jdk "OracleJDK8"
    }
    environment {
        CENTRAL-REPO='vpro-maven-central'
        NEXUS-GRP-REPO='vpro-maven-group'
        NEXUS-PASS='Dattatreya2!'
        NEXUS-USER='admin'
        RELEASE-REPO='vprofile-release'
        SNAP-REPO='vprofile-snapshot'
        NEXUSIP='172.31.8.5'
        NEXUSPORT='8081'
        NEXUS-GRP-REPO ='vpro-maven-group'
    }
    stages{
        stage("Build"){
            steps{
                sh 'mvn -s settings.xml -DskipTests install'
            }
           
        }
    }
    
}
pipeline{
    agent any 
    tools {
        maven "MAVEN3"
        jdk "OracleJDK8"
    }
    environment {
        CENTRAL_REPO='vpro-maven-central'
        NEXUS_GRP_REPO='vpro-maven-group'
        NEXUS-PASS='Dattatreya2!'
        NEXUS_USER='admin'
        RELEASE_REPO='vprofile-release'
        SNAP_REPO='vprofile-snapshot'
        NEXUSIP='172.31.8.5'
        NEXUSPORT='8081'
        NEXUS_GRP_REPO ='vpro-maven-group'
    }
    stages{
        stage("Build"){
            steps{
                sh 'mvn -s settings.xml -DskipTests install'
            }
           
        }
    }
    
}
pipeline{
    agent any 
    tools {
        maven "MAVEN3"
        jdk "OracleJDK8"
    }
    environment {
        CENTRAL_REPO='vpro-maven-central'
        NEXUS_GRP_REPO='vpro-maven-group'
        NEXUS_PASS='Dattatreya2!'
        NEXUS_USER='admin'
        RELEASE_REPO='vprofile-release'
        SNAP_REPO='vprofile-snapshot'
        NEXUSIP='172.31.8.5'
        NEXUSPORT='8081'
    
    }
    stages {

        stage("Build"){
            steps{
                sh 'mvn -s settings.xml -DskipTests install'
            }

            post {
                success {

                    echo "Successful build"
                    archiveArtifacts artifacts: '**/*.war'
                }
            }

             
           
           
        }

    stage('Test') {
        steps {
            sh 'mvn test'
        }
 
    }

    stage('Checkstyle Code Analysis') {
            steps {
                sh 'mvn checkstyle:checkstyle'
            }
    }

    }
    
}
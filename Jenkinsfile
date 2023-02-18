pipeline {

    agent any 
    tools {
        // Whereever maven is there use this. 
        // Use this for jdk. 
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
        SONARSERVER = 'sonarserver'
        SONARSCANNER = 'sonarscanner'
        NEXUSLOGIN = 'nexuslogin'
    
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
                sh 'mvn -s settings.xml checkstyle:checkstyle'
            }
    }

     stage('Sonar Analysis') {

        environment {
            scannerHome = tool "${SONARSCANNER}"
        }
        steps {
            
        withSonarQubeEnv("${SONARSERVER}") {

            sh '''${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=vprofile \
            -Dsonar.projectName=vprofile \
            -Dsonar.projectVersion=1.0 \
            -Dsonar.sources=src/ \
            -Dsonar.java.binaries=target/test-classes/com/visualpathit/account/controllerTest/   \
            -Donar.junit.reportsPath=target/surefire-reports/ \
            -Dsonar.jacoco.reportPath=target/jacoco.exec \
            -Dsonar.java.checkstyle.reportPaths=target/checkstyle-result.xml
            '''
            }
            
        }
    } 

    stage("Deploy Artefact to Jenkins") {
    steps {
    nexusArtifactUploader(
        nexusVersion: 'nexus3',
        protocol: 'http',
        nexusUrl: "${NEXUSIP}:${NEXUSPORT}",
        groupId: 'QA',
        version: "${env.BUILD_ID}-${env.BUILD_TIMESTAMP}",
        repository: "${RELEASE_REPO}",
        credentialsId: "${NEXUSLOGIN}",
        artifacts: [
            [artifactId: 'vproapp',
             classifier: '',
             file: 'target/vprofile-v2.war',
             type: 'war']
        ]
     )

    }

    }
}

   
 
}

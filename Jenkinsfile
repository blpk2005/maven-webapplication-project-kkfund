node {

    def MavenHome = tool name: "maven-3.9.16"

    stage("Git checkout/ cloning") {
        git branch: 'main',
            url: 'https://github.com/blpk2005/maven-webapplication-project-kkfund.git'
    }

    stage("Compile") {
        sh "${MavenHome}/bin/mvn compile"
    }
    stage("Build creation"){
        sh "${MavenHome}/bin/mvn clean package"
    }
    stage("Sonarqube report"){
        sh "${MavenHome}/bin/mvn sonar:sonar"
    }
    stage("Artifact backup"){
        sh "${MavenHome}/bin/mvn deploy"
    }
    stage("Deploy"){
        sh """
        curl -u admin:admin \
--upload-file ${WORKSPACE}/target/maven-web-application.war \
"http://32.198.19.198:8080/manager/text/deploy?path=/maven-web-application&update=true"
        """
    }
}

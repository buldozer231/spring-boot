
def REPO_URL = "https://github.com/buldozer231/spring-boot/"
def POM_PATH = "spring-boot/spring-boot-tests/spring-boot-smoke-tests/spring-boot-smoke-test-web-ui/pom.xml"
def BUILD_VERSION = '1.0.'+env.BUILD_NUMBER
def IMAGE_PATH    = 'spring-boot/spring-boot-tests/spring-boot-smoke-tests/spring-boot-smoke-test-web-ui/target/spring-boot-smoke-test-web-ui-2.2.1.BUILD-SNAPSHOT.jar'
def ARTIFACT_ID = "spring-boot"
def NEXUS_REPO = "maven-releases"
def NEXUS_URL = "34.70.39.207"
def NEXUS_PORT = "80"
def NEXUS_GROUP = "graduation"
def ARTIFACT_NAME = "spring-boot"


withCredentials([usernameColonPassword(credentialsId: 'e56b0ea0-d636-4532-9f7a-8e542fa16760', variable: 'nexus-credentials')]) {
    // some block
}

node () {
    stage ("CHECKOUT") {
        // sh "pwd"
        sh "rm -rf spring-boot/"
        sh "git clone ${REPO_URL}"
    }
    stage ("BUILD") {
       withMaven(
            maven: 'Maven') {
            sh "mvn clean install -e -f ${POM_PATH}"
        }
    }
    stage ("UPLOAD ARTIFACT") {
        nexusArtifactUploader(
            nexusVersion: 'nexus3',
            protocol: 'http',
            nexusUrl: "${NEXUS_URL}:${NEXUS_PORT}",
            groupId: "${NEXUS_GROUP}",
            version: "${BUILD_VERSION}",
            repository: "${NEXUS_REPO}",
            credentialsId: 'e56b0ea0-d636-4532-9f7a-8e542fa16760',
            artifacts: [
                [artifactId: "${ARTIFACT_ID}",
                classifier: '',
                file: "${IMAGE_PATH}",
                type: 'jar']
            ]
        )
    }

    // stage ("Build Docker image") {
    //     sh "wget --user=admin --password=1Vfrcbv53 http://${NEXUS_URL}/repository/${NEXUS_REPO}/${NEXUS_GROUP}/${ARTIFACT_ID}/${BUILD_VERSION}/"
    //     sh "cd /ansible && ansible-playbook -l devtools buildDocker.yml"
    //     sh "docker build -t buldozer232/spring-boot"
    // }
    //34.70.39.207/repository/
    //maven-releases/Graduation/spring-boot/1.0.48/spring-boot-1.0.48.jar

    stage ("CI DEPLOY") {
        build 'CI-deploy'
    }
    stage ("QA DEPLOY") {
        build 'QA-deploy'
    }

}

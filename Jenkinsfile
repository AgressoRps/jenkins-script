node {
    stage ('Clone') {
        git url: 'git@github.com:AgressoRps/JavaWebIntro-1.git'
    }
 
    stage('Gradle Build') {
        if (isUnix()) {
        sh './gradlew clean build'
        } else {
            bat 'gradlew.bat clean build'
        }
    }
    stage('archive'){
        archive 'build/**/*.jar'
    }
    stage('NexusArtifactUploaderJob') {
        nexusArtifactUploader(
            nexusVersion: 'nexus3',
            protocol: 'http',
            nexusUrl: '172.23.0.3:8081',
            groupId: 'com.starokozhev',
            version: '0.0.1-dev.27+5df023f',
            repository: 'maven-releases',
            credentialsId: '07399129-bce1-4983-ad4f-eb5111694103',
            artifacts: [
                [artifactId: 'JavaWebIntro-1',
                 classifier: '',
                 file: './build/libs/JavaWebIntro-0.0.1-dev.27.uncommitted+5df023f.jar',
                 type: 'jar']
            ]
        )
    }
}